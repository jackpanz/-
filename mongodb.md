## 用户权限
~~~sql
use admin;

db.createUser({
	user: "admin",
	pwd: "admin",
	roles: [{
		role: "root",
		db: "admin"
	}]
})

db.grantRolesToUser("admin", [{
	role: "root",
	db: "admin"
}, {
	role: "readWrite",
	db: "test"
}])

db.updateUser("admin", {
	roles: [{
		role: "userAdminAnyDatabase",
		db: "admin"
	}, {
		role: "readWrite",
		db: "dzswjdbtar"
	}]
});

db.auth("admin","admin");

show users;
~~~

删除数据库
~~~sql
db.dropDatabase() 
~~~

删除表
~~~sql
db.表名.drop()
~~~

* 数据库用户角色：read、readWrite; 
* 数据库管理角色：dbAdmin、dbOwner、userAdmin；
* 集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager； 
* 备份恢复角色：backup、restore； 
* 所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase 
* 超级用户角色：root 

## 插入
~~~sql
> db.student.insert({id:1,name:"张三",gender:"男",age:18})
WriteResult({ "nInserted" : 1 })

> db.student.save({id:2,name:"李四",gender:"男",age:19})
WriteResult({ "nInserted" : 1 })

> db.student.insertOne({id:3,name:"王五",gender:"男",age:18})
{
	"acknowledged" : true,
	"insertedId" : ObjectId("62986a0622e54ae6c619dde6")
}

db.student.insertMany(
... [
... {id:4,name:"赵六",gender:"女",age:21},
... {id:5,name:"钱七",gender:"女",age:20}
... ]
... )
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("62986bbe22e54ae6c619dde8"),
		ObjectId("62986bbe22e54ae6c619dde9")
	]
}
~~~

## 查询

* db.student.find()
* db.student.findOne({id:5})
* db.student.find({id:3})

* AND 					find({条件,条件,条件})
* OR 						find({$or:[{条件},{条件},{条件}]})
* 
| &nbsp;        | &nbsp;        |
| ------------- | ------------- |
|查询条件|
|等于|{\<key\>:\<value\>}
|不等于|{\<key\>:{$ne:\<value\>}}
|小于|{\<key\>:{$lt:\<value\>}}
|小于或等于|{\<key\>:{$lte:\<value\>}}
|大于|{\<key>:{$gt:\<value\>}}
|大于或等于|{\<key\>:{$gte:\<value\>}}
|不等于|{\<key\>:{$ne:\<value\>}}
|in|{\<key\>:{$in:[\<value\>,\<value\>\<value\>,\<value\>]}}
|not in|{\<key\>:{$nin:[\<value\>,\<value\>,\<value\>,\<value\>]}}
|like|{\<key>:\/\<value\>\/}<br/>{\<key\>:\/\^\<value\>\/}<br/>{\<key\>:\/\<value\>\^\/}
|&nbsp;|&nbsp;
|只显示某些字段|find({},{name:1,age:1})
|不显示某些字段|find({},{name:0})
|&nbsp;|&nbsp;
|排序|find({}.sort({age:1})<br/>find({}.sort({age:0})									
|&nbsp;|&nbsp;
|limit|find().limit(5)
|查询7条以后的数据|find().skip(7)
|查询在3-12之间的数据|find().skip(2).limit(8)
|&nbsp;|&nbsp;
|count|find().count()
|&nbsp;|&nbsp;
|$exists判断字段是否存在|find({age:{$exists:true}})<br/>find({age:{$exists:false}})
|&nbsp;|&nbsp;					
|$mod取模运算|find({age:{$mod:[5,3]}})


子对象查询
~~~json
{
	"name": "njy",
	"spec": {
		"weight": 200,
		"area": "taiwang"
	}
}
~~~
~~~sql
db.shop.find({'spec.area':'hanguo'})
~~~

子数组查询
~~~json
{
	"name": "njy",
	"hobby": ["aaa", "bbb", "ccc"]
}
~~~
~~~sql	
find({hobby:"fight"})
~~~

子数组对象查询
~~~json
{
	"_id": "123",
	"name": "人文医学",
	"qList": [{
			"qid": 1,
			"content": "医学伦理学的公正原则",
			"reorderFlag": 1
		},
		{
			"qid": 2,
			"content": "制定有关人体实验的基本原则",
			"reorderFlag": 0
		}
	]
}
~~~
~~~sql		
{ "qList": { $elemMatch: { "qid": 1, "reorderFlag": 0} } }
~~~ 
 


## 修改
### db.表.update({条件},{'$set' :{字段:值,字段:值}})
### db.表.update({条件},{字段:值,字段:值}) 
* 有$set的修改：只修改设置的字段，其他字段不变
* 没有$set的修改：只修改设置的字段，没有修改的字段就删除了（_id除外)
	
## 删除操作	
### 删除记录：db.表.remove(条件)					
