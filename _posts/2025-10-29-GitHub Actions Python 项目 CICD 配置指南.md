---
title: GitHub Actions Python 项目 CI/CD 配置指南
description: >-
  本文整理了 Python 项目在 GitHub Actions 中从拉取代码到运行脚本的完整配置方案，包含基础版、优化版，兼顾易用性和性能，可直接复制复用。
date: 2025-08-09 20:55:00 +0800
categories: [GitHub Actions, 教程]
tags: [教程]
---

本文整理了 Python 项目在 GitHub Actions 中从拉取代码到运行脚本的完整配置方案，包含基础版、优化版，兼顾易用性和性能，可直接复制复用。

## 一、拉取仓库代码

### 核心说明

`actions/checkout@v5` 是拉取仓库代码的标准动作，`fetch-depth` 控制克隆深度，`token` 用于扩展权限，按需选择配置即可。

### 基础版(仅拉取最新代码，无需历史提交/分支，自动使用 `GITHUB_TOKEN)

```yaml
- name: 拉取仓库代码（基础版）
  uses: actions/checkout@v5
```

### 优化版(需要操作历史提交、切换分支、读取标签、生成版本号等场景)

```yaml
  - name: 拉取仓库代码
    uses: actions/checkout@v5
    with:
      token: ${{ secrets.GH_PAT }}  # 你的PAT密钥
      fetch-depth: 0  # 拉取完整历史
```

### 关键参数说明

1. `fetch-depth: 0` 适用场景（非必要不使用）：
   - 需执行 `git log`/`git describe` 查看历史提交/版本标签；
   - 需切换到非当前触发分支（如从 main 切到 dev）；
   - 项目包含子模块，或需基于提交历史生成版本号（如 poetry/setuptools-scm）。
2. `token: GH_PAT` 适用场景：
   - 默认 `GITHUB_TOKEN` 权限不足（如跨仓库操作、触发嵌套工作流）；
   - 需**推送代码回仓库、访问私有仓库**等进阶操作。
3. 性能提示：`fetch-depth: 1` 克隆速度最快，`0` 会增加耗时（v5 版本比 v4 快 10-20%）。

## 二、配置 Python 环境

### 基础版（核心功能）

```yaml
- name: 配置Python环境
  uses: actions/setup-python@v6
  with:
    python-version: '3.11'  # 推荐字符串格式，避免YAML解析异常
```

### 优化版（推荐，含缓存）

```YAML
- name: 配置Python环境（带缓存）
  uses: actions/setup-python@v6
  with:
    python-version: '3.11'
    cache: 'pip'  # 缓存依赖包，大幅加速安装（核心优化）
    # 可选：依赖文件非根目录时指定路径
    # cache-dependency-path: 'src/requirements.txt'
```

### 关键说明

- `python-version` 支持格式：`3.11`（自动装最新补丁版）、`3.11.8`（精确版本）、`3.x`（最新 3 系）；
- `cache: pip` 自动识别 `requirements.txt`/`pyproject.toml` 等文件，仅依赖变更时重新下载。

## 三、安装依赖

### 场景 1：单包/少量包安装（基础版）

适用于仅需安装个别依赖的场景，优先升级 pip 避免兼容问题：

```YAML
- name: 安装依赖（单包）
  run: |
    python -m pip install --upgrade pip  # 必做：升级pip
    pip install requests pandas  # 安装多个包
    # 生产环境推荐指定版本：pip install requests==2.31.0 pandas==2.1.4
```

### 场景 2：批量依赖安装（通用版，推荐）

通过 `requirements.txt` 统一管理依赖，配合 pip 缓存效率更高：

```YAML
- name: 安装依赖（批量）
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt  # 安装所有依赖
    pip list  # 可选：验证安装结果
```

### 配套操作（本地生成 requirements.txt）

```Bash
# 导出当前环境已安装的所有包及版本
pip freeze > requirements.txt
```

### 优化技巧（国内环境）

添加镜像源加速下载，解决安装超时问题：

```YAML
- name: 安装依赖（国内镜像加速）
  run: |
    python -m pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple/
    pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/
```

## 四、运行 Python 脚本

### 场景 1：运行单个脚本（基础版）

```YAML
- name: 运行Python脚本
  run: |
    # 脚本路径：仓库根目录/scripts/preprocess.py
    python scripts/preprocess.py
```

### 场景 2：运行多个脚本（按顺序）

```YAML
- name: 运行多个脚本
  run: |
    # 按执行顺序编写，Linux路径用/分隔（区分大小写）
    python scripts/preprocess.py  # 预处理
    python scripts/main.py        # 主逻辑
    python scripts/validate.py    # 结果验证
```

### 场景 3：带参数/环境变量运行（进阶）

```YAML
- name: 运行脚本（带参数/环境变量）
  env:
    # 传递环境变量（脚本内用 os.getenv("API_KEY") 获取）
    API_KEY: ${{ secrets.API_KEY }}
    ENV: "production"
  run: |
    # 传递命令行参数
    python scripts/main.py --input data.csv --env $ENV
```

### 关键注意事项

1. 路径：Linux 系统区分大小写（如 `Scripts/PreProcess.py` ≠ `scripts/preprocess.py`）；
2. 权限：无需给脚本加执行权限（`chmod +x`），通过 Python 解释器运行即可；
3. 验证：建议添加结果检查，确保脚本运行符合预期：

   ```YAML
   - name: 运行脚本（带结果验证）
     run: |
       python scripts/preprocess.py
       # 检查脚本生成的文件是否存在
       if [ -f "scripts/output.csv" ]; then
           echo "脚本运行成功"
       else
           echo "脚本运行失败"
           exit 1  # 终止工作流并标记失败
       fi
   ```

## 五、推送文件

```YAML
      - name: 推送文件
        run: |
          git config --global user.name "更新机器人"
          git config --global user.email "software-bot@github.com"

          find . -type f -size +100M -print0 | xargs -0 rm -f
          echo "✅ 已清理超过100MB的文件"
          
          git add .
          git commit -a -m "Update $(date +'%Y-%m-%d %H:%M:%S')" || echo "No changes to commit"
          git push
```

```YAML
      - name: 设置提交时间
        run: |
          echo "COMMIT_TIME=Update: $(TZ='Asia/Shanghai' date +'%Y-%m-%d %H:%M:%S')" >> $GITHUB_ENV

      - name: 推送文件
        uses: EndBug/add-and-commit@v10
        with:
          message: ${{ env.COMMIT_TIME }}
          committer_name: GitHub Actions
          committer_email: actions@github.com
```  

## 六、完整工作流示例（可直接复用）

### 执行脚本

```YAML
name: main
on:
  workflow_dispatch:
  schedule:
    - cron: '0 6 * * *'  # 每日UTC6点（北京时间14点）执行

jobs:
  main:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5

      - name: Setup Python
        uses: actions/setup-python@v6
        with:
          python-version: '3.x'
          cache: 'pip'
          
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.tx

      - name: 执行更新脚本
        run: |
          python subscribe/collect.py
```

### 执行脚本并推送

```YAML
name: main
on:
  workflow_dispatch:
  schedule:
    - cron: '0 6 * * *'  # 每日UTC6点（北京时间14点）执行

jobs:
  main:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout
        uses: actions/checkout@v5

      - name: 配置Python环境
        uses: actions/setup-python@v6
        with:
          python-version: '3.14'
          cache: 'pip'
          # 可选：依赖文件非根目录时指定路径
          cache-dependency-path: 'code/requirements.txt'
          
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r code/requirements.txt

      - name: 执行更新脚本
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}  # 内置Token（API调用）
        run: |
          python code/autocrx.py

      - name: 提交更新文件（普通推送）
        run: |
          git config --global user.name "更新机器人"
          git config --global user.email "software-bot@github.com"

          find . -type f -size +100M -print0 | xargs -0 rm -f
          echo "✅ 已清理超过100MB的文件"
          
          git add .
          git commit -a -m "Update $(date +'%Y-%m-%d %H:%M:%S')" || echo "No changes to commit"
          git push
```

### 测试

```YAML
name: test

on:
  push:
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout
        uses: actions/checkout@v5

      - name: 生成/修改文件
        run: |
          echo "自动生成的文件" > auto-generated-file.txt
          date > last-update.txt

      - name: 设置提交时间
        run: |
          echo "COMMIT_TIME=Update: $(TZ='Asia/Shanghai' date +'%Y-%m-%d %H:%M:%S')" >> $GITHUB_ENV

      - name: 提交并推送文件
        uses: EndBug/add-and-commit@v10
        with:
          message: ${{ env.COMMIT_TIME }}
          committer_name: GitHub Actions
          committer_email: actions@github.com
```  

## 总结

1. 拉取代码：基础场景用 `fetch-depth: 1`，需历史操作时用 `0`，权限不足时加 `GH_PAT`；
2. 配置环境：优先用 `setup-python@v6 + cache: pip`，大幅提升依赖安装速度；
3. 安装依赖：推荐用 `requirements.txt` 批量管理，国内环境添加镜像源；
4. 运行脚本：路径区分大小写，建议添加结果验证，确保流程可靠性。
