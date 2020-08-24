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



