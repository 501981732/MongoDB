

##   安装配置见 vue2自学中 node+vue+mongoDB

>    show databases
    
>    use demo-1(数据库名称 切换/创建数据库)

>    db.dropDatabase()删除数据库
    
>    show tables

>    db.col.drop() 删除集合col
- 增删改查

    - 增
    >   db.col.insert({title: 'MongoDB 教程', xxx}) 向col集合中插入数据
    
    > 3.2之后 db.col.insertOne({"a": 3}) 插入一条
    
    > db.col.insertMany([{"b": 3}, {'c': 4}]) 插入多条
    
    - 删
    
    > db.col.deleteMany({}) 删除全部文档
    
    > db.col.deleteMany({ status : "A" })  删除status等于A的全部文档
    
    > db.col.deleteOne( { status: "D" } )  删除status等于A的一个文档
    
    > db.col.remove({})
    
    - 改
    
    > 3.2版本开始 db.collection.updateOne() 向指定集合更新单个文档
    
        db.test_collection.updateOne({"name":"abc"},{$set:{"age":"28"}})
    
    > db.collection.updateMany() 向指定集合更新多个文档
    
    - 查
    
    >  db.col.find().pretty()
    
    > AND语句  db.col.find({key1:value1, key2:value2}).pretty()
    
    > OR语句  db.col.find({$or:[{"key1":"2333"},{"title": "MongoDB 教程"}]}).pretty()
    
    > 连用  db.col.find({"likes": {$gt:50}, $or: [{"by": "2333"},{"title": "MongoDB 教程"}]}).pretty()
    
    > db.collection.find(query, projection) 
    
        db.collection.find(query, {title: 1, by: 1}) // inclusion模式 指定返回的键，不返回其他键
        
        db.collection.find(query, {title: 0, by: 0}) // exclusion模式 指定不返回的键,返回其他键
        
        

- 条件操作符实例

        
```
$gt -------- greater than  >
$gte --------- gt equal  >=
$lt -------- less than  <
$lte --------- lt equal  <=
$ne ----------- not equal  !=
$eq  --------  equal  =
```

        db.col.find({"likes" : {$gt : 100}})  likes大于100    对应于SQL中的     Select * from col where likes > 100;
        
        db.col.find({likes : {$gte : 100}})  likes大于等于100    对应于SQL中的     Select * from col where likes >= 100;
        
        db.col.find({likes : {$lt :200, $gt : 100}})             对应于SQL中的   Select * from col where likes>100 AND  likes<200;
        
- limit 和 skip

        db.col.find({},{"title":1,_id:0}).limit(1).skip(2)   第一个 {} 放 where 条件，为空表示返回集合中所有文档。第二个 {} 指定那些列显示和不显示 （0表示不显示 1表示显示)

- sort 排序

        db.col.find().sort({KEY:1})  1 为升序排列，而-1是用于降序排列

- 索引：高效查询 索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构
- 
        db.COLLECTION_NAME.ensureIndex({KEY:1})    Key 值为你要创建的索引字段，1为指定按升序创建索引，如果你想按降序来创建索引指定为-1即可。

- 聚合 (aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。有点类似sql语句中的 count(*)。

        db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
    eg:
    
        db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}]) ===>SQL
        select by_user as _id, count(*) as num_tutorial from mycol group by by_user
        
        