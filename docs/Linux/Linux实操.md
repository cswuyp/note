* [1.如何查找出现频率最高的100个ip地址](#1-如何查找出现频率最高的100个ip地址)
* [2.查看文件的前n行和后n行命令](#2-查看文件的前n行和后n行命令)

# 1. 如何查找出现频率最高的100个ip地址
#cat access_log |cut -d ' ' -f 1 |sort |uniq -c | sort -nr | awk '{print $0 }' | head -n 10 |less

# 查看文件的前n行和后n行命令
查看文件/etc/profile的前10行内容
```
# head -n 10 /etc/profile
```
查看文件etc/profile的后10行内容
```
# tail -n 10 /etc/profile
```
如果想同时查看可以将前10行和后5行的显示信息通过输出重定向的方法保存到一个文档，这样查看文档即可一目了然。
```
# head -n 10 /etc/profile>>/home/test
# tail -n 10 /etc/profile>>/home/test
```
查看的话只需要打开test文件即可
```
cat /home/test
```
从第3000行开始，显示1000行，即显示3000-3999行
```
cat filename|tail -n +3000|head -n 1000
```
显示1000行到3000行
```
cat filename|head -n 3000|tail -n +1000
```
分解：  
```
tail -n 1000:显示最后1000行
tail -n +1000:从1000行开始显示
head -n 1000:显示前面1000行
```
