PreparedStatement
=================
是一种特殊的“语句”类。
- Statement类执行的语句只能是静态的字符串 
- PreparedStatement类执行的语句可以含有变量（采用占位符思想实现）

## 头文件
```cpp
#include <cppconn/prepared_statement.h>
```
## 类
```cpp
PreparedStatement *pstmt;
// 创建对象
pstmt = con->prepareStatement("INSERT INTO test(id, label) VALUES(?, ?)");
```
通过Connector对象的prepareStatement函数来创建该类对象。其参数是一个含有占位符（**?**）的SQL语句。
### 填充占位符
```cpp
pstmt->setInt(1, 2);       // 给第一个占位符填充数字2
pstmt->setString(2, "b");  // 给第二个占位符填充字符串"b"
```
### 执行SQL
```cpp
pstmt->execute();
```

## Demo
```cpp
#include <iostream>

#include <mysql_driver.h>
#include <mysql_connection.h>
#include <cppconn/prepared_statement.h>
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

    con->setSchema("test");
    PreparedStatement *pstmt;
    pstmt = con->prepareStatement("INSERT INTO test(id, label) VALUES(?, ?)");
    if (!pstmt)
    {
        cout<<"prepared stmt error"<<endl;
        return -1;
    }
    pstmt->setInt(1, 2);
    pstmt->setString(2, "b");
    pstmt->execute();

    delete pstmt;
    delete con;
}
```
