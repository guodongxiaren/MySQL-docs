Statement
=========
执行SQL语句的类
## 头文件
```cpp
#include <cppconn/statement.h>
```
## 类
是一个接口类。只包含纯虚函数。
```cpp
sql::Statement *stmt;
// 创建对象
stmt = con->createStatement();
```
### 成员函数
```cpp
	virtual bool excute(const sql::SQLString& sql) = 0;
```
## Demo
```cpp
#include <iostream>

#include <mysql_driver.h>
#include <mysql_connection.h>
#include <cppconn/statement.h>
using namespace std;
using namespace sql;
int main()
{
    mysql::MySQL_Driver *driver;
    Connection *con;

    driver = mysql::get_mysql_driver_instance();
    if (!driver)
    {
        cout<<"dirver error"<<endl;
        return -1;
    }

    con = driver->connect("tcp://127.0.0.1:3306", "root", "123456");
    if (!con)
    {
        cout<<"conn error"<<endl;
        return -1;
    }

    Statement *stmt;
    stmt = con->createStatement();
    if (!stmt)
    {
        cout<<"stmt error"<<endl;
        return -1;
    }
	// 执行各种SQL语句
    stmt->execute("USE test");                                   // 选择数据库
    stmt->execute("DROP TABLE IF EXISTS test");                  // 如果表已存在，则删除
    stmt->execute("CREATE TABLE test(id INT, label CHAR(1))");   // 创建表
    stmt->execute("INSERT INTO test(id, label) VALUES(1, 'a')"); //插入数据

    delete stmt;
    delete con;
}
```
