- npm install mongodb


- 插入数据


```
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/elm'; # 数据库为 elm
 
var insertData = function(db, callback) {  
    //连接到表 site
    var collection = db.collection('site');
    //插入数据
    var data = [{"name":"222","url":"www.222.com"},{"name":"333","url":"www.333.com"}];
    collection.insert(data, function(err, result) { 
        if(err)
        {
            console.log('Error:'+ err);
            return;
        }     
        callback(result);
    });
}
 
MongoClient.connect(DB_CONN_STR, function(err, db) {
    console.log("连接成功！");
    insertData(db, function(result) {
        console.log(result);
        db.close();
    });
});
```
- 查找数据库


```
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/elm';    
 
var selectData = function(db, callback) {  
  //连接到表  
  var collection = db.collection('site');
  //查询数据
  var whereStr = {"name":'wm'};
  collection.find(whereStr).toArray(function(err, result) {
    if(err)
    {
      console.log('Error:'+ err);
      return;
    }     
    callback(result);
  });
}
 
MongoClient.connect(DB_CONN_STR, function(err, db) {
  console.log("连接成功！");
  selectData(db, function(result) {
    console.log(result);
    db.close();
  });
});
```
- 更新数据


```
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/elm';    
 
var updateData = function(db, callback) {  
    //连接到表  
    var collection = db.collection('site');
    //更新数据
    var whereStr = {"name":'elm'};
    var updateStr = {$set: { "url" : "https://www.elm.com" }};
    collection.update(whereStr,updateStr, function(err, result) {
        if(err)
        {
            console.log('Error:'+ err);
            return;
        }     
        callback(result);
    });
}
 
MongoClient.connect(DB_CONN_STR, function(err, db) {
    console.log("连接成功！");
    updateData(db, function(result) {
        console.log(result);
        db.close();
    });
});
```
- 删除数据


```
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/runoob';    
 
var delData = function(db, callback) {  
  //连接到表  
  var collection = db.collection('site');
  //删除数据
  var whereStr = {"name":'elm'};
  collection.remove(whereStr, function(err, result) {
    if(err)
    {
      console.log('Error:'+ err);
      return;
    }     
    callback(result);
  });
}
 
MongoClient.connect(DB_CONN_STR, function(err, db) {
  console.log("连接成功！");
  delData(db, function(result) {
    console.log(result);
    db.close();
  });
});
```
