MongoDB安装:
======
- ####下载: 从官网上下载,配置环境变量.
- ####MongoDB的启动:</br>
在cmd命令中`mongod --dbpath 数据库的存放路径`
- ####在新cmd窗口中输入 `mongo` (未设置用户名密码时) or `mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]`进入数据库
- ####MongoDB命令<br>

命令 | 作用 
--|---
show dbs | 显示数据库
use XX | 使用数据库(没有则创建)
db | 查看数据库
db.XX.insert({"name":"yy"})|插入数据
db.dropDatabase() | 删除数据库(先进入此数据库)
db.createCollection(name ,options) | 创建集合
show collections | 显示集合
db.collectionName.drop() | 删除集合
db.collectionName.insert()  | 插入集合
db.collectioName.find().pretty() | 查找所有插入的数据并整理
db.collectionName.update({"name": "XX"},{$set: {"sd" : "sad"}})|更新
db.collectionName.deleteOne({}) | 删除一个集合
db.collectionName.deleteMany({}) | 删除多个集合
db.colName.find({attr : $lt}) | 选择查询
$gt | greater than  >
$gte | gt equal  >=
$lt | less than  <
$lte | lt equal  <=
$ne | not equal  !=
$eq |  equal  =

