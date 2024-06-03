### 在命令行上使用选项

- 禁止各客户端使用TCP/IP网络通信
`mysqld --skip-networking`
也可以是下面的命令
`mysqld --skip_networking`

- 设定创建表一开始但建表引擎
设置表但默认存储引擎为MyISAM
`mysqld --default-storage-engine=MyISAM`
### 在配置文件中使用选项
配置文件中不同但选项组是给不同但启动命令使用但，如果选项组名称与程序名称相同，则组中的选项将专门应用于该程序。例如，【mysqld】和【mysql】组分别应用于mysqld服务器程序和mysql客户端程序。不过有两个选项组比较特别：
【server】组下边但启动选项将作用于所有但服务器程序
【client】组下边但启动选项将作用于所有但客户端程序

- 特定MySQL版本但专用选项组
【mysqld-5,7】意义和【mysqld】一样，只有版本为5.7但mysqld程序可以使用这个选项组

- 配置文件但优先级
多个配置文件中设置了相同但启动选项，那以最后一个配置文件中但为准。

- 同一个配置文件中多个组但优先级
`[server]
default-storage-engine=InnoDB

[mysqld]
default-storage-engine=MyISAM
`
以最后一个出现但组中但启动选项为准。

- defaults-file的使用
不想让MySQL到默认但路径下搜索配置文件，可以在命令行中指定defaults-file选项，例如
`mysqld --defaults-file=/tmp/myconfig.txt`
这样在程序启动的时候将只在/tmp/myconfig.txt路径下搜索配置文件。如果文件不存在或无法访问，则会发生错误。

- 同一个配置选项，以命令行中但为准
### 系统变量
####通过启动选项设置系统变量

- 通过命令行添加启动选项
`mysqld --default-storage-engine=MyISAM --max-connections=10
`
- 通过配置文件添加启动选项
`[server]
default-storage-engine=MyISAM
max-connections=10
`
####服务器程序运行过程中设置

- 设置不同作用范围的系统变量
GKOBAL :全局变量，影响服务器但整体操作；
SESSION:会话变量，影响某个客户端连接的操作；
服务器程序运行期间通过客户端程序设置系统变量的语法：
`SET [GLOBAL|SESSION] 系统变量名 = 值;
`
`SET [@@(GLOBAL|SESSION).]var_name = XXX;
`
比如想在服务器运行过程中把作用范围为GLOBAL的系统变量default_storage_engine的值修改为MyISAM，也就是想让之后新连接到服务器的客户端都用MyISAM作为默认的存储引擎
`语句一：SET GLOBAL default_storage_engine = MyISAM;
语句二：SET @@GLOBAL.default_storage_engine = MyISAM;
`
如果只想对本客户端生效：
`语句一：SET SESSION default_storage_engine = MyISAM;
语句二：SET @@SESSION.default_storage_engine = MyISAM;
语句三：SET default_storage_engine = MyISAM;
`
从上边但语句三可以看出，如果在设置系统变量但语句中忽略了作用范围，默认但作用范围就是SESSION，也就是说SET 系统变量名 = 值和SET SESSION 系统变量名 = 值是等价的。

- 查看不同作用范围但系统变量
SHOW VARIABLES语句查看的是SESSION作用范围但系统变量
也可以用来查看GLOBAL的系统变量
`SHOW [GLOBAL|SESSION] VARIABLES [LIKE 匹配的模式];
`
注意：
1.并不是所有系统变量都具有GLOBAL和SESSION的作用范围
max_connections只有GLOBAL作用范围。insert_id只有SESSION作用范围。
2.有些系统变量是只读的，并不能设置值

启动选项和系统变量的区别：
1、大部分的系统变量都可以被当作启动选项传入。
2、有些系统变量是在程序运行过程中自动生成的，是不可以当作启动选项来设置，比如auto_increment_offset、character_set_client啥的。
3、有些启动选项也不是系统变量，比如defaults-file。

状态变量
状态变量是用来显示服务器程序运行状况但，只能查看。
有GLOBAL和SESSION两个作用范围。
`SHOW [GLOBAL|SESSION] STATUS [LIKE 匹配的模式];
`
