MySQL Connector/C++接口编程
============================
## 头文件路径
```
include/
├── cppconn
│   ├── build_config.h
│   ├── config.h
│   ├── connection.h
│   ├── datatype.h
│   ├── driver.h
│   ├── exception.h
│   ├── metadata.h
│   ├── parameter_metadata.h
│   ├── prepared_statement.h
│   ├── resultset.h
│   ├── resultset_metadata.h
│   ├── sqlstring.h
│   ├── statement.h
│   ├── variant.h
│   ├── version_info.h
│   └── warning.h
├── mysql_connection.h
├── mysql_driver.h
└── mysql_error.h
```
## 编译环境
需要存在boost库。  
一种可能g++的编译选项：

```makefile
CFLAGS  =  -I/usr/local/mysql/include \
           -I/usr/local/boost/include \
           -L/usr/local/boost/lib \
           -L/usr/local/mysql/lib \
           -Wl,-rpath=/usr/local/mysql/lib \
           -lmysqlcppconn \
```
如果mysql的库路径没有被编辑在**/etc/ld.so.conf.d/**目录中（要有root权限，并用ldconfig命令刷新）的话，  
则需要用**-Wl,-rpath**选项指定。
