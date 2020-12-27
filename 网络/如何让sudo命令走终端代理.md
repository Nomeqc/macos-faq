# 如何让sudo命令走终端代理
## 问题描述：
执行命令让终端命令走代理：
```bash
export http_proxy="http://127.0.0.1:8001"; export HTTP_PROXY="http://127.0.0.1:8001"; export https_proxy="http://127.0.0.1:8001"; export HTTPS_PROXY="http://127.0.0.1:8001"
```
执行命令`curl www.google.com`，正常返回内容

执行以下命令`curl`
```bash
sudo /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/AloneMonkey/MonkeyDev/master/bin/md-update)"
```
发现`curl`下载速度感人

## 分析
加了`sudo`后`curl`命令没有走代理

## 解决
1. 找到`/etc/sudoers`文件，右键`简介` -> 修改`everyone`权限为读和写
2. 用`sublime text` 打开文件，在在最后一行`Defaults	env_keep +=`的下一行添加`Defaults	env_keep += "http_proxy https_proxy no_proxy"`
3. 最后，修改`everyone`权限为只读。
> 注意空格，否则执行sudo命令会提示语法错误
## 效果
执行:
```bash
sudo /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/AloneMonkey/MonkeyDev/master/bin/md-update)"
```
`curl`终于走代理了，速度显著提升~
