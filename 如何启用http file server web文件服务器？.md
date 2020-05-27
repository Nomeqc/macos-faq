* ### 1. 开启HTTP服务
```shell
sudo apachectl start 
```
* ### 2. `cd`带要共享的目下，输入命令：
python2:
```bash
python -m SimpleHTTPServer 
```
python3:
```shell
# 9999为端口号
python3 -m http.server 9999
```
* ### 3. 浏览器输入`http://127.0.0.1:8000`就可以看到共享的内容了。
