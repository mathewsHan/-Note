kotlin  的main函数  可以独立于 Class文件之外
/* 简洁性 :   空安全:  ？符 toast (user?.name）   易扩展 toast
 
 */ 
 基本数据类型  
	 另外如果不需要参数或者只需要一个参数时
	class User {
	var name: String? = null
	var id: String? = null

	constructor(name: String) {
	this.name = name
	}

	constructor(name: String, id: String) {
	this.name = name
	this.id = id
	}
	}

作者：罗拙呓
链接：https://www.jianshu.com/p/3d2c0c92f545
来源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。

与java 定义完全一样  只是·  Float(精确到小数点后  6位 )Long Double 大写 

var 关键字

var   b:Boolean  = false
j
	kotlin 调用 java 
	只能类型推断 且转换

kotlin  不用写分号   而且编译器就解决 空判断问题,避免空指针
	
kotlin  类型强制转换
to方法基本数据类型转换

var s = "10" 
s.toInt()
s.toByte()

10可以转成任何数据类型的 10 

不同数据类型 不能相互赋值 

/*******常量********
const    等价于java    piblic  static  
>
>/和  var 

//--------字符串(模板性)-----------------
trimIndent()原样输出字符串















