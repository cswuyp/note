* [cJSON](#cjson)
  * [cJSON语法规则](#cjson语法规则)
  * [cJSON结构体](#cjson结构体)




# cJSON
 cJSON是一种轻量级的数据交换格式
 
# cJSON语法规则
数据在名称/值对中  
数据由括号分隔  
大括号保存对象  
中括号保存数组  

cJSON值可以是：
（1）数字（整数或浮点数）
```c++
{"age":30}
```
（2）字符串(在双引号中)
```c++
{"name":"brook"}
```
（3）逻辑值（true或false）
```c++
{"flag":true}
```
（4）对象（在大括号中）
```c++
对象可以包含对个key/value（键/值）对。
```
（5）数组（在中括号中）
```c++
{
"sites":[
{"name":"wuyepeng","url":"https://github.com/cswuyp"},
{"name":"baidu","url":"www.baidu.com"},
{"name":"google","url":"wwwgoogle.com"}
]
}
```
解析：    
上面的例子中，对象“sties”是包含三个对象的数组。

（6）null  
```c++
{"runoob":null}
```

#cJSON结构体
cJSON是c语言中的一个JSON编辑器，在一些面向对象的编程语言中，存在字符串数组、字典等数据结构，可以非常方便地对JSON数据进行处理，而c语言只能使用JSON数据
