# Go Web 编程笔记
来源于 [https://astaxie.gitbooks.io/build-web-application-with-golang/zh/](https://astaxie.gitbooks.io/build-web-application-with-golang/zh/)

## Go语言基础

### Go基础
对于`slice`，`append`函数会改变slice所引用的数组的内容，从而影响到引用同一数组的其它`slice`。 但当`slice`中没有剩余空间（即(cap-len) == 0）时，此时将动态分配新的数组空间。返回的`slice`数组指针将指向这个空间，而原数组的内容将保持不变；其它引用此数组的`slice`则不受影响。

`map`和其他基本型别不同，它不是`thread-safe`，在多个`go-routine`存取时，必须使用`mutex lock`机制

`make`用于内建类型（`map`、`slice` 和`channel`）的内存分配。`new`用于各种类型的内存分配。

传指针有什么好处呢？  
- 传指针使得多个函数能操作同一个对象。
- 传指针比较轻量级 (8bytes),只是传内存地址，我们可以用指针传递体积大的结构体。如果用参数值传递的话, 在每次copy上面就会花费相对较多的系统开销（内存和时间）。所以当你要传递大的结构体的时候，用指针是一个明智的选择。
- Go语言中channel，slice，map这三种类型的实现机制类似指针，所以可以直接传递，而不用取地址后传递指针。（注：若函数需改变slice的长度，则仍需要取地址传递指针）

### 流程和函数

### struct

### 面向对象
> "A method is a function with an implicit first argument, called a receiver."
> 
method的语法如下：

    func (r ReceiverType) funcName(parameters) (results)

指针作为receiver  
不用担心你是调用的指针的method还是不是指针的method，Go知道你要做的一切  
也就是说：
> 如果一个method的receiver是*T,你可以在一个T类型的实例变量V上面调用这个method，而不需要&V去调用这个method

类似的
> 如果一个method的receiver是T，你可以在一个T类型的变量P上面调用这个method，而不需要 P去调用这个method



### interface
interface是一组method签名的组合，我们通过interface来定义对象的一组行为。  
interface类型定义了一组方法，如果某个对象实现了某个接口的所有方法，则此对象就实现了此接口。  
如果我们定义了一个interface的变量，那么这个变量里面可以存实现这个interface的任意类型的对象。

一个函数把interface{}作为参数，那么他可以接受任意类型的值作为参数，如果一个函数返回interface{},那么也就可以返回任意类型的值。

Go语言实现了反射，所谓反射就是能检查程序在运行时的状态。我们一般用到的包是reflect包。


### 并发

## Web基础

### Web 工作方式
HTTP协议是无状态的和Connection: keep-alive的区别  
无状态是指协议对于事务处理没有记忆能力，服务器不知道客户端是什么状态。从另一方面讲，打开一个服务器上的网页和你之前打开这个服务器上的网页之间没有任何联系。  
HTTP是一个无状态的面向连接的协议，无状态不代表HTTP不能保持TCP连接，更不能代表HTTP使用的是UDP协议（面对无连接）。  
从HTTP/1.1起，默认都开启了Keep-Alive保持连接特性，简单地说，当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的TCP连接。  
Keep-Alive不会永久保持连接，它有一个保持时间，可以在不同服务器软件（如Apache）中设置这个时间。  


## session和数据存储
### session和cookie
session和cookie的目的相同，都是为了克服http协议无状态的缺陷，但完成的方法不同。session通过cookie，在客户端保存session id，而将用户的其他会话消息保存在服务端的session对象中，与此相对的，cookie需要将所有信息都保存在客户端。因此cookie存在着一定的安全隐患，例如本地cookie中保存的用户名密码被破译，或cookie被其他网站收集（例如：1. appA主动设置域B cookie，让域B cookie获取；2. XSS，在appA上通过javascript获取document.cookie，并传递给自己的appB）。


