# 什么是http？作用是什么?
- http是hyper-text transfer protocol,超文本传入协议；是一种客户端和服务器端进行文件传输通信的协议

# http的请求和响应的内容称之为‘报文’，请问报文的结构是什么？
HTTP 有两类报文：

- 请求报文----从客户向服务器发送请求报文,见图6-12(a).

- 响应报文----从服务器到客户的回答，见图6-12(b).


![img](../img/http.PNG)


由于 HTTP是面向文本的(text-oriented),因此在报文中的每一个字段都是一些ASCII码串，因而每个字段的长度都是不确定的。


HTTP请求报文和响应报文都是由三个部分组成。
## 可以看出，这两种报文格式的区别就是<b>开始行</b>不同。
(1) 开始行 用于区分是请求报文还是响应报文。

- 在请求报文中的开始行叫做请求行(Request-Line)
	- 请求报文的开始行叫请求行：方法+空格+URL+空格+HTTP版本+CRLF
		- 方法：
			OPTION:请求一些选项的信息
			GET：请求读取URL的信息
			HEAD：读取URL信息的首部
			POST：给服务器添加信息
			PUT：在URL下存储一个文档
			DELETE：删除url下的资源
			TRACE：进行环回测试的请求报文
			CONNECT：代理服务器
- 而在响应报文中的开始行叫做状态行(Staus-Line).
	- 响应报文的开始行叫状态行：版本+空格+状态码+短语+CRLF
- 在开始行的三个字段之间都以空格隔开
- 最后的“CR”和“LF”分别表示“回车”和“换行”。

(2)首部行 用来说明浏览器，服务器或报文主体的一些信息。

- 首部可以有好几行，也可以不使用。
- 在每一个首部行中都有首部字段名和它的值，每一行在结束的地方都要有“回车”和“换行”。
- 整个首部行结束时，还有一空行将首部行和后面的实体主体分开
- 
(3)实体主体 在请求报文中一般都不用这个字段，而在响应报文中也可能没有这个字段。

# 在看看HTTP响应报文的主要特点。
每一个请求报文发出后，都能收到一个响应报文，响应报文的第一行就是状态行。
状态行包含三项内容：HTTP的版本，状态码，以及解释状态码的简单语句。
状态码都是三位数字的，分为5大类共33种。例如：

- 1xx 表示通知信息的，如请求收到了或正在进行处理。
- 2xx 表示成功，如接受或是知道了。
- 3xx 表示重定向，如要完成请求还必须采取下一步的行动。
- 4xx 表示客户的差错，如请求中有错误的语法或不能完成。
- 5xx 表示服务器的差错，如服务器失效无法完成请求。

# 总结：
1.请求报文和响应报文的结构都是：开始行+首部行+实体主体
2.请求报文的开始行叫请求行Request-line，由请求方式，URL和http版本号三部分构成。
3.响应报文的开始行叫状态行status-line，由http版本号，状态码和状态码的简单短语描述构成。

# 关于编码
## 常用的对特殊字符进行编码和解码的函数，在js中有三种：
- encodeURI / decodeURI
- encodeURIComponent / decodeURIComponent
- escape / unescape

## 使用场景和说明：
- 1. escape是对字符串(string)进行编码(而另外两种是对URL)，作用是让它们在所有电脑上可读。
- 2. encodeURI 不会转义url中有特殊含义的字符，比如url和query parameter之间的？符号，又比如query parameter之间的&符号和=

		var test ="http://www.cnblogs.com/season-huang/p/3439277.html?name=pis&age=18"
		// 可以看见html后面有个？连接url和查询变量
		// 查询变量之间有赋值的=号和连接多个变量的&号
- 3.encodeURIComponent 会对所有的特殊字符进行转义
		
		var test="http://www.cnblogs.com/season-huang/p/3439277.html? name=pis&age=18 "
		encodeURI(test) // "http://www.cnblogs.com/season-huang/p/3439277.html?%20name=pis&age=18%20"
		encodeURIComponent // "http%3A%2F%2Fwww.cnblogs.com%2Fseason-huang%2Fp%2F3439277.html%3F%20name%3Dpis%26age%3D18%20"

## 使用场景说明

1. 从上面的例子中可以看出这三个方法的区别

- 如果你单纯的想对字符串进行编码解码。和url没有毛线关系，那就用escape和unescape
- 如果你想解析url中的传入的变量，那么使用encodeURIComponent，因为它转码的范围比较大，包括了？&等url中有特殊含义的字符都会被转义
- 如果你想解析整个url，那就推线使用encodeURI
