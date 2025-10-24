---
date: 2025-08-19
title: 便携版Git(git-portable)的使用与配置
---
## 下载安装

你需要从 Git 官网或镜像网站下载 Git 便携版 [PortableGit-2.51.1-64-bit.7z.exe](https://registry.npmmirror.com/-/binary/git-for-windows/v2.51.1.windows.1/PortableGit-2.51.1-64-bit.7z.exe)

Git 官网 https://git-scm.cn/downloads/win

 [镜像网站](https://registry.npmmirror.com/binary.html?path = git-for-windows/)

## 修改用户目录

在 `安装目录/etc/bash.bashrc` 文件末尾追加：

```bash
export HOME=/workdir/ 
cd workdir
```

## 密钥修改

ssh 的密钥对与配置文件默认在 C:/Users/[username]/.ssh 目录下，同样不利于前面提到的对 git 便携要求。

如果需要让 `~/.ssh/config` 中的密钥生效（例如多仓库用不同密钥）直接配置为：

```
git config --global core.sshCommand "ssh -F ~/.ssh/config"
```

## git init 命令与 git clone 命令

创建本地仓库的方法有两种：

- 一种是创建全新的仓库：`git init`，会在当前目录初始化创建仓库，也可指定目录：`git init [文件目录]` 执行命令后，如下显示

  ```bash
  git init project
  ```

其中“project”是文件目录，会自动创建。创建完多出了一个被隐藏的.git 目录，这就是本地仓库 Git 的工作场所

- 另一种是克隆远程仓库：`git clone [url]` 克隆远程仓库，如在 github 上创建的仓库

  ```bash
  git clone https://github.com/kwonganding/KWebNote.git
  ```


## git add 命令

**git add** 命令可将该文件的修改添加到暂存区。通过运行 **git add** 命令，你可以告诉 Git 哪些文件的修改应该包含在下一次提交（commit）中。

添加一个或多个文件到暂存区：

  ```bash
git add [file1] [file2] ...
  ```

添加指定目录到暂存区，包括子目录：

  ```bash
git add [dir]
  ```

添加当前目录下的所有文件到暂存区：

  ```bash
git add .
  ```

命令用于查看项目的当前状态。

  ```bash
git status -s
  ```

## git commit 命令

提交暂存区到本地仓库中: [message] 可以是一些备注信息。

  ```bash
git commit -m [message]
  ```

**-a** 参数设置修改文件后不需要执行 git add 命令，直接来提交。命令格式如下：

  ```bash
git commit -a
  ```

## git push 命令


**git push** 命令用于从将本地的分支版本上传到远程并合并。

命令格式如下：

  ```bash
git push <远程主机名> <本地分支名>:<远程分支名>
  ```

如果本地分支名与远程分支名相同，则可以省略冒号：

  ```bash
git push <远程主机名> <本地分支名>
  ```

## git pull 命令


**git pull** 命令用于从远程获取代码并合并本地的版本。

**git pull** 其实就是 **git fetch** 和 **git merge** 的简写，先从远程仓库获取最新的提交记录，然后将这些提交记录合并到你当前的分支中。

命令格式如下：

  ```bash
git pull [远程仓库名] [分支名]
  ```

- `[远程仓库名]` 通常是 `origin`，是默认的远程仓库名。
- `[分支名]` 是你要合并的远程分支，比如 `main` 或 `master`。

## Git 提交信息编辑

这是 Git 的 **提交信息编辑界面**（默认用 Vim 编辑器打开），需要你输入本次提交的说明（描述你修改/新增了什么内容），然后保存退出即可完成提交。

### 操作步骤

1. **进入编辑模式**：按键盘上的 `i` 键（左下角会显示 `-- INSERT --`，表示可以输入文字）。
2. **输入提交信息**：在第一行输入有意义的描述（比如新增了 EmEditor 相关配置文档），示例：

 ```Plain
 新增 EmEditor 配置说明文档
 ```

注意：不要以 `#` 开头（会被 Git 忽略），空消息会取消提交。

3. **退出编辑模式**：按键盘上的 `Esc` 键（左下角 `-- INSERT --` 消失）。
4. **保存并退出**：输入 `:wq`（冒号 + w + q，w = 保存，q = 退出），然后按回车键。
   如果不想提交了，按 `Esc` 后输入 `:q!`（冒号 + q + !，! 表示强制退出不保存），按回车键即可取消本次提交。

### 效果说明

输入完成后，Git 会将本次 `git add .` 暂存的文件（这里是新增的 `EmEditor/配置说明文档.md`）提交到本地仓库，之后就可以执行 `git push -u origin main` 推送到远程 GitHub 了。

### 提交信息建议

尽量简洁明了，说明“做了什么”，比如：

- 新增：`新增 EmEditor 配置文档`
- 修改：`优化 EmEditor 配置说明的格式`
- 删除：`删除无用的 EmEditor 旧配置文件`

这样后续查看提交历史（`git log`）时，能快速知道每次提交的目的。
