# kotlin基本数据类型
```kotiln
Double  64
Float	32
Long    64
Int     32
Short	16
Byte    8
```

# 静态变量或常量
```kotiln
class A {
    companion object {
        //静态变量 可以改变
        var URL1: String = "URL1"
        //常量
        val URL2: String = "URL2"
        //常量 相当于加了private和get方法取值
        const val URL3: String = "URL3"
        //常量 懒加载
        val URL4: String by lazy {
            var value:String = URL2 + URL3
            value
        }
    }
}
```

# 属性
```kotiln
val attr: Int = 0
//getter setter
val attr: Int = 0
    get() {
        println("---get---")
        return field
    }
    set(value) {
        println("---set---")
    }
//属性继承 open声明可继承，override声明继承属性
open val attr: Int = 1
override val attr: Int = 2
//延迟加载 只能修饰,非kotlin基本类型
lateinit val attr: String
```

# 类构造方法
```kotiln
//相当于constructor(param:String)
class A (param:String){
 init{
  println("init")
  println("param:"+param)
 }
}
class A (){
 init{
  println("init")
 }
 constructor(){
 }
}
```
## 多个构造方法
```kotiln
class AA:A{
 init{
  println("init")
 }
 //私有的构造方法
 private constructor(){
 }
 //可以调用父类的构造方法
 constructor(param:String):super(){
 }
 //可以调用本类的其他构造方法
 constructor(param1:String,param2:String):this(param1){
 }
}
```



