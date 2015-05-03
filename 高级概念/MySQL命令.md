MYSQL命令
=======
##登陆命令
    mysql -u用户名 -p密码
用户名和-u选项之间可以有空格，但是密码和-p选项之间必须无空格。但是这样密码会是明文。你可以在键入-p之后，回车再输入密码，就是密文。
###常用选项

|缩写|全写|描述
|----|---|---
|-h|--host|主机
|-p|--password|密码
|-P|--port|端口
|-V|--version|版本信息
|-u|--user|用户
||--prompt|修改提示符

####--prompt
--prompt 支持几个转义词组
* \h 主机名
* \D 完整日期
* \d 当前数据库
* \u 当前用户

##登陆之后
###退出
* exit
* quit
* \q

都能退出mysql，系统显示Bye。
###帮助
键入`help`或`\h`。
###显示信息
select:
* version(); 版本信息
* now(); 当前时间
* user(); 用户@主机名

###使用系统命令
**\!** 后加shell命令可以在mysql中执行shell命令。
>gdb使用shell加命令来执行shell命令。
