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



