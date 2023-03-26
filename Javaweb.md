# Javaweb

### HTTP

浏览器和服务器之间传输数据的规则



**请求格式**

分为3部分:

1. 请求行

   ```
   GET /路径 HTTP/1.1
   请求方式/资源路径 协议版本 (注意每部分之间都有一个空格)

2. 请求头

   ```
   //key: value格式的
   Host: 请求的主机名
   User-Agent: 浏览器版本
   Accept: 能接收的资源类型
   Accept-Language: 偏好语言
   Accept-Encoding: 可以支持的压缩类型

3. 请求体

   ```
   //POST请求的参数 与请求头要空一行
   username=superbaby&password=123456

get请求的参数在url之后衔接  以?隔开,参数之间以&隔开  (url有长度限制,参数也不能无限)

post请求  可以无限参数



**响应分类**

1. 响应行

   ```
   HTTP/1.1 200 OK
   协议版本 状态码 状态码描述

2. 响应头

   ```
   key:value
   Content-Type: 响应内容的类型(text/html/image)
   Content-Length: 内容长度(字节数)
   Content-Encoding: 压缩算法
   Cache-Control: 如何缓存max-age=300 最多缓存300秒

3. 响应体:存放响应数据( 格式由Content-Type决定 )



### Web服务器/Tomcat

1. 封装HTTP操作
2. 将Web项目部署到服务器中



将网页项目放到webapps的目录下,启动startup.bat

服务启动  通过localhost:端口号/项目/文件名来访问



一般JavaWeb项目会被打包成war包,放到webapp下,Tomcat会自动解压缩



### Maven

创建后自己在src下创建文件夹:main/java   main/resources   test/java   test/resources

idea自动关联这些文件

在pom.xml的目录中

- mvn clean：清理

- mvn compile：编译主程序

- mvn test-compile：编译测试程序

- mvn test：执行测试

- mvn package：打包

- mvn install：安装

  

自己的项目文件放到webapp目录中

该目录里的WEB-INF文件夹中的web.xml是该项目配置文件



打包后变成这个目录,就可以部署到Tomcat了

![image-20230114181320368](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230114181320368.png)



### Servlet

**什么是servlet和容器**

直接与客户端打交道的是Tomcat(容器).它监听端口,请求过来后,根据url等信息,确定将请求交给哪个servlet处理. servlet自身就是个用service函数来提供服务的小家伙

而(大写的s)Servlet接口就是这些小家伙的规范,方便容器去管理他们

ps.由于Tomcat同时也处理http之类的事情,所以Tomcat是Web服务器+Servlet容器,tql!

基本步骤:

![image-20230114194859913](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230114194859913.png)

注意,爆红就重新加载一下

1. pom中导入 //pom是这个项目的配置文件,不管是插件还是版本啥的都可以在这里面处理
2. 重写这些方法:
   - init()   主要是为了让Servlet对象在处理客户请求前可以完成一些初始化工作，例如：建立数据库的连接，获取配置信息等
   - service()  
   - destroy()
   - getServletConfig()
   - getServletInfo()

3. @WebServlet注解作用跟配置文件差不多

   比如上面的/demo1代表访问这个Servlet的网址是[localhost:8888/MavenTest/demo1](http://localhost:8888/MavenTest/demo1)

   (MavenTest是项目名称, 且不一定要是项目名称,可以改 )



#### Servlet执行流程

沿着url层层访问到Servlet类

1. 第一次被访问时,由Servlet容器来创建Servlet对象

2. 其中一个ServletConfig对象包含配置信息,调用init()方法初始化,传入配置信息

3. 每次处理Servlet请求时, 容器都会调用service方法处理请求

4. 关闭容器时就调用destroy( )释放内存

web服务器(Tomcat)自动执行类中的方法



在@WebServlet中,loadOnStartup属性: 负数表示有请求的时候创建对象(默认) 正数或0表示服务器启动时就创建,从0开始依次创建.



### 现在开始吧

　HttpServlet 指能够处理 HTTP 请求的 servlet，它在原有 Servlet 接口上添加了一些与 HTTP 协议处理方法，它比 Servlet 接口的功能更为强大。因此开发人员在编写Servlet时，通常**应继承这个类，而避免直接去实现Servlet接口。**

我们只需要继承HttpServlet,重写doGet和doPost, 就可以处理请求了

urlPattern配置规则:

![image-20230115000049507](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115000049507.png)



```
public void service
(ServletRequest servletRequest, ServletResponse servletResponse)
```

这是service的两个参数,

一个是Request,是客户端发过来的,

一个是Response,是我们要回应过去的

1. 获取Request请求数据

![image-20230115004247743](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115004247743.png)

用这些方法解析Request请求

对于参数,还有这些方法

Map< String,String[] > getParameterMap(): 获取所有参数的map集合

String[] getParameterValues(String name) :根据名称获取参数值

String getParameter(String name): 获取参数值( 单个 )



POST中文乱码: request.setCharacterEncoding("UTF-8/GBK") 总之换一下

GET中文乱码:

**请求转发**

一个请求处理一部分之后 交给另一个类去处理.

request.GetRequestDispatcher( "类的路径").forward( request,response );

![image-20230115020535932](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115020535932.png)

上面的方法都是request类的

2. response

这是一些方法

![image-20230115021806903](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115021806903.png)

其中第二个也有一个addheader,可以不重写



重定向Redirect  

请求一个资源时,不是该网页,但你知道要转到令一个网址

```
response.setStatus(302) //设置响应状态码302,
response.setHeader("Location","路径") //设置响应头Location:路径,指定要跳转的
```

或者一个简单的方法:

response.sendRedirect("路径")

原理是响应一个数据回去,让他知道这是302,这样就可以跳转了

**路径问题**

虚拟目录:    /项目名   ( 资源对应的项目 )

目录:  /资源名

浏览器使用: 虚拟目录           比如html中的链接,是浏览器发出的

服务端使用: 不加虚拟目录    比如自己的方法参数( 除了浏览器相关方法 )

通过request.getContextPath( )获取虚拟目录,再用"+"号和目录连接,是一种动态页面的方式



**设置response**

一旦涉及输入输出,将数据转换为流

写响应体:

PrintWriter writer = response.getWriter( )       //字符流

或者ServletOutputStream  so =response.getOutputStream( )  //字节流

然后 writer.write( )  或so.write( )

响应体的格式可以是html,只要在响应头中设置Content-Type为text/html即可



中文乱码: response.setContentType( "text/html; character=utf-8 " )

这个方法可直接设置Content-Type



字节流拷贝:

原始方式:一个输入流read到一个byte[]中,while返回值len≠-1,输出流就来读取0到len的byte[]

封装: 首先在pom中添加依赖:commons-io 

IOUtils.copy( 输入流, 输出流 )