* [get和post的区别](#get和post的区别)
* [get和post的应用场景](#get和post的应用场景)
* [关于HTTP协议](https://www.jianshu.com/p/80e25cb1d81a)
* [HTTP面试都问啥](https://mp.weixin.qq.com/s?__biz=MzUyNjQxNjYyMg==&mid=2247484857&idx=2&sn=1753c5630a98be4141796606f5ad7061&chksm=fa0e6a38cd79e32e44cc046dc68576f26c9fc71eb341c9648d28107277fbc0556989c07ffb13&scene=0&key=7462c83afda42677b06c5a0246ee1c85e2d74046017fea8427dcb7bcab46c2c40e3da2959c76ae48c005e7bd6010479d3f0d7f723b6da0f4e371029c214c3f0904947263cb2d4d26b17bd93d013e48c3&ascene=14&uin=MjEzMDkzMzUwNA%3D%3D&devicetype=Windows+7&version=62060728&lang=zh_CN&pass_ticket=j5C66yru4LWtCVCeCOMbUc%2FXqNumswxmjPHDkg0m0n7e6JMVHbFMAFXv1XFSocMQ)
* [HTTP和HTTPS](#http和https)

# get和post的区别
POST和GET都是向服务器提交数据，并且都会从服务器获取数据。

区别：

1、传送方式：get通过地址栏传输，post通过报文传输。

2、传送长度：get参数有长度限制（受限于url长度），而post无限制

3、GET和POST还有一个重大区别，简单的说：

GET产生一个TCP数据包；POST产生两个TCP数据包
长的说：

对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；
而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。
也就是说，GET只需要汽车跑一趟就把货送到了，而POST得跑两趟，第一趟，先去和服务器打个招呼“嗨，我等下要送一批货来，你们打开门迎接我”，然后再回头把货送过去。
因为POST需要两步，时间上消耗的要多一点，看起来GET比POST更有效。因此Yahoo团队有推荐用GET替换POST来优化网站性能。但这是一个坑！跳入需谨慎。为什么？
1. GET与POST都有自己的语义，不能随便混用。
2. 据研究，在网络环境好的情况下，发一次包的时间和发两次包的时间差别基本可以无视。而在网络环境差的情况下，两次包的TCP在验证数据包完整性上，有非常大的优点。
3. 并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次。
建议：

1、get方式的安全性较Post方式要差些，包含机密信息的话，建议用Post数据提交方式；

2、在做数据查询时，建议用Get方式；而在做数据添加、修改或删除时，建议用Post方式；

案例：一般情况下，登录的时候都是用的POST传输，涉及到密码传输，而页面查询的时候，如文章id查询文章，用get 地址栏的链接为：article.php?id=11，用post查询地址栏链接为：article.php， 不会将传输的数据展现出来。

拓展资料：

GET在浏览器回退时是无害的，而POST会再次提交请求。

GET产生的URL地址可以被Bookmark，而POST不可以。

GET请求会被浏览器主动cache，而POST不会，除非手动设置。

GET请求只能进行url编码，而POST支持多种编码方式。

GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。

GET请求在URL中传送的参数是有长度限制的，而POST么有。

对参数的数据类型，GET只接受ASCII字符，而POST没有限制。

GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。

GET参数通过URL传递，POST放在Request body中。

#  get和post的应用场景 
get和post两种方法都是将数据发送到服务器，HTTP标准包含这两种方法是为了达到不同的目的。

post用于创建资源，资源的内容会被编入HTTP请示的内容中，例如，处理订货单、在数据库中加入数据行等。

当请求无 副作用时（如进行搜索），便可用get方法，当请求有副作用时（如添加数据行）则用post方法。一个比较实际的问题是：get方法可能会产生很长的url，或许会超过某些服务器对url长度的限制。

若符合下列任一情况，则用post方法：  
1.请求的结果有持续性的副作用，例如：数据库内添加新的数据行。  
2.若使用get方法，则表单上收集的数据可能让url过长。  
3.要传送的数据不是采用7位的ASCII编码。

若符合下列任一情况，则用get方法：  
1.请求时为了查找资源，HTML表单数据仅用来帮组搜索。  
2.请求结果无持续性的副作用。  
3.收集的数据及HTML表单内的输入字段名称的总长度不超过1024个字符。

操作方式|数据位置|明文密文|数据安全|长度限制|应用场景
  ---|:--:|:--:|:--:|:--:|---:
  get|HTTP报头|明文|不安全|长度较小|数据查询
  post|HTTP正文|可明可密|安全|支持较大数据传输|修改数据

# HTTP和HTTPS
HTTP的全称是Hyper Text Transfer Protocol,中文名叫作超文本传输协议。HTTP协议是用于从网络传输超文本数据到本地浏览器的传送协议，它能保证高效的而准确的传送超文本文档。HTTP由万维网协会和Internet工作小组IETF共同合作制定的规范，目前广泛使用的是HTTP1.1版本。  

HTTPS的全称是Hyper Text Transfer Protocol over Secure Socket Layer,是以安全为目标的HTTP通道，简单讲是HTTP的安全版，即HTTP下加入SSL层，简称为HTTPS。  

HTTPS的安全基础是SSL，因此通过它传输的内容是经过SSL加密的，它的主要作用可以分为两种。  
1.建立一个信息安全通道来保证数据传输的安全。  
2.确认网站的真实性，凡是使用了HTTPS的网站，都可以通过点击浏览器地址栏的锁头标志来查看网站认证之后的真实信息，也可以通过CA机构颁发的安全签章来查询。

有一些网站虽然使用了HTTPS协议，但是还是会被浏览器提示不安全，例如我们的12306，这是因为12306的CA证书是中国铁道部自行签发的，而这个证书不被CA机构信任所以就会出现“您的连接不是私密连接”。  


