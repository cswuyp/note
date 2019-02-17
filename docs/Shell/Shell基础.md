* [查找指定文件或目录](#查找指定文件或目录)

# 查找指定文件或目录
```
find [命令选项] [路径] [表达式选项]
```

查找当前目录下名称为hello.txt的文档
```
find -name hello.txt
```

查找/root目录下所有名称以.log结尾的文件
```
find /var/log/ -name "*.log"
```
