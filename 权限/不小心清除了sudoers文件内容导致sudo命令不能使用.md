# 不小心清除了`/etc/sudoers`文件内容导致`sudo`不能使用
## 解决：
1. `/etc/sudoers`文件右键 -> `简介` -> 修改`everyone`权限为读和写
2. 从苹果开源库中下载 `sudoers`默认内容。[下载](https://opensource.apple.com/source/sudo/sudo-86/files/sudoers) 
3. 将内容写入`/etc/sudoers`
4. `/etc/sudoers`文件右键 -> `简介` -> 修改`everyone`权限为只读
