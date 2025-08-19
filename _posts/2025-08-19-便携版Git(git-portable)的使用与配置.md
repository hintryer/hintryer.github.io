---
date:2025-08-19
title:便携版Git(git-portable)的使用与配置
---
## 下载安装
你需要从Git官网或镜像网站下载Git便携版
Git官网  https://git-scm.cn/downloads/win
镜像网站


## 修改用户目录

在`安装目录/etc/bash.bashrc`文件末尾追加：
```
#  user add 231215
export HOME=/workdir/
# the home directory is in gitdir/home/[username]
# your need create the folder first
```

## windows 下 git ssh 的目录修改以及多 ssh key 设置

ssh 的密钥对与配置文件默认在 C:/Users/[username]/.ssh 目录下，同样不利于前面提到的对 git 便携要求。

```
git config --global core.sshCommand "ssh -i ~/.ssh/id_rsa_example -F ~/.ssh/config"
```
