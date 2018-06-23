ResultSet
=========
SQL语句返回的结果集
## 头文件
```cpp
#include <cppconn/resultset.h>
```
## 创建对象
由`sql::Statement::executeQuery()`和`sql::PreparedStatement::executeQuery()`返回。
比如：
```
sql::Connection *con;
sql::Statement *stmt;
sql::ResultSet *res;
// ...
con->setSchema("test");
// ...
stmt = con->createStatement();
res = stmt->executeQuery("SELECT id, label FROM test");
```
## 成员函数
### next
返回bool类型，用于**逐行**遍历结果集。  

结果集内部有**游标**，标记着当前行。游标起始位置为第一行，每次执行完next函数，游标都会移动到下一行。
## getXXX
|函数|返回值|说明
|-----|-----|-----
|getInt|int32_t|返回当前行某一列的值作为整型
|getString|SQLString|返回当前行某一列值作为字符串
|getUInt|uint32_t|......32位无符号整型
|getInt64|int64_t|......64位有符号整型
|getUInt64|uint64_t|......64位无符号整型
|getBoolean|bool|......bool类型
|getBlob|std::istream|.......二进制类型

**getXXX**是一系列函数，用于取出当前行某一列值。**XXX**表示数据类型。

该系类函数有两个重载：
- 可以用整型作为参数，表示取第几列的值。
- 也可以使用字符串作为参数，取出对应列名的值。

比如
```
while (res->next())
{
	cout << "id = "<<res->getInt(1)<<";label = "<<res->getString("label")<<endl;
}
```
