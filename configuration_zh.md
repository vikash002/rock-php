
# 在哪修改？ #

使用编辑器（比如notepad或者VI/VIM命令）打开RockMongo安装目录下的\_config.php_，所有的配置都在这里。_

# 认证 #

## mongo\_auth 和control\_auth ##
在开始使用RockMongo之前，你需要决定使用哪种校验方式。

如果mongo\_auth被设成了true，用户必须使用MongoDB中的用户名和密码（由命令db.addUser()添加），所以配置中的mongo\_user, mongo\_pass和mongo\_db就不再需要了，因为用户可以通过界面输入这些信息。

如果control\_auth被设置了true，而且mongo\_auth设成了false，用户必须根据control\_users选项的配置进行登录，mongo\_user, mongo\_pass和mongo\_db就生效了。为了安全起见，安装完毕之后，应该尽快将默认的用户名和密码改成一个较为复杂的用户名和密码。

如果mongo\_auth和control\_auth都被设置了false，则用户无需用户名和密码即可登录。


### mongo\_auth示范 ###
你使用MongoDB的用户名、密码和数据库名进行登录：

```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
$MONGO["servers"][$i]["mongo_port"] = "27017";
$MONGO["servers"][$i]["mongo_timeout"] = 0;
$MONGO["servers"][$i]["mongo_auth"] = true;//启用MongoDB校验
$i ++;
```

### control\_auth示范 ###
你使用control\_users中的配置进行登录。

```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
$MONGO["servers"][$i]["mongo_port"] = "27017";
$MONGO["servers"][$i]["mongo_timeout"] = 0;
//$MONGO["servers"][$i]["mongo_db"] = "MONGO_DATABASE";
//$MONGO["servers"][$i]["mongo_user"] = "MONGO_USERNAME"
//$MONGO["servers"][$i]["mongo_pass"] = "MONGO_PASSWORD";
$MONGO["servers"][$i]["mongo_auth"] = false;//禁用MongoDB校验

$MONGO["servers"][$i]["control_auth"] = true;//启用登录控制校验
$MONGO["servers"][$i]["control_users"]["admin"] = "admin";
$MONGO["servers"][$i]["control_users"]["iwind"] = "123456";//在下面可以复制更多的用户
$i ++;
```

### 无认证示范 ###
你无需任何用户名和密码即可登录。

```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
$MONGO["servers"][$i]["mongo_port"] = "27017";
$MONGO["servers"][$i]["mongo_timeout"] = 0;
//$MONGO["servers"][$i]["mongo_db"] = "MONGO数据库名";
//$MONGO["servers"][$i]["mongo_user"] = "MONGO用户名"
//$MONGO["servers"][$i]["mongo_pass"] = "MONGO密码";
$MONGO["servers"][$i]["mongo_auth"] = false;//禁用MongoDB校验

$MONGO["servers"][$i]["control_auth"] = false;//禁用登录控制校验
$i ++;
```

# Mongo #

## mongo\_name ##
v1.1. mongo服务器名字，可以是一个易懂的名字
```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
```

## mongo\_host ##
v1.1. mongo主机地址
```
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
```

## mongo\_port ##
v1.1. mongo端口
```
$MONGO["servers"][$i]["mongo_port"] = "27017";
```

## mongo\_db ##
v1.1. 默认连接的数据库名称，只有mongo\_auth=false的时候生效。
```
$MONGO["servers"][$i]["mongo_db"] = "my_own_database";
```

## mongo\_user ##
v1.1. mongo authentication user name, works only if mongo\_auth=false.
```
$MONGO["servers"][$i]["mongo_user"] = "";
```

## mongo\_pass ##
v1.1. mongo authentication password, works only if mongo\_auth=false
```
$MONGO["servers"][$i]["mongo_pass"] = "";
```

## mongo\_auth ##
v1.1. enable mongo authentication? If the option is enabled, you have to log-in the system with your account and password added in MongoDB.
```
$MONGO["servers"][$i]["mongo_auth"] = false;
```

## mongo\_timeout ##
v1.1. mongo connection timeout, set as "0" for never timeout.
```
$MONGO["servers"][$i]["mongo_timeout"] = 0;
```

The issue with long-running query: [http://code.google.com/p/rock-php/issues/detail?id=177](http://code.google.com/p/rock-php/issues/detail?id=177)

## mongo\_options ##
v1.1.1. mongo connection options
```
$MONGO["servers"][$i] = array("replicaSet" => "xxxxx");
```

# Controls #
## control\_auth ##
v1.1. enable control users, works only if mongo\_auth=false
```
$MONGO["servers"][$i]["control_auth"] = true;
```

## control\_users ##
v1.1. one of control users [USERNAME](USERNAME.md)=PASSWORD, works only if mongo\_auth=false
```
$MONGO["servers"][$i]["control_users"]["myusername"] = "mypassword";
$MONGO["servers"][$i]["control_users"]["iwind"] = "123456";
```


# UI #
## ui\_only\_dbs ##
v1.1. databases to display, can be a string or an array. If this list is not empty, then databases not in this list all will be invisible.
```
$MONGO["servers"][$i]["ui_only_dbs"] = "admin,local";//a string
$MONGO["servers"][$i]["ui_only_dbs"] = array( "admin", "local" );//an array
```

## ui\_hide\_dbs ##
v1.1. databases to hide, can be a string or an array.
```
$MONGO["servers"][$i]["ui_hide_dbs"] = "shop,merchant";//a string
$MONGO["servers"][$i]["ui_hide_dbs"] = array("shop", "merchant");//an array
```

## ui\_hide\_collections ##
v1.1. collections to hide, can be a string or an array, each collection name can be a valid regular expression:
```
$MONGO["servers"][$i]["ui_hide_collections"] = "users,admins";//hide users and admins colleciton
$MONGO["servers"][$i]["ui_hide_collections"] = "mail_(.*)";//hide all collections whose prefix is "mail_"
```

## ui\_hide\_system\_collections ##
v1.1. if we should hide system collections, such like system.js, system.indexes, etc. Set to false as default.
```
$MONGO["servers"][$i]["ui_hide_system_collections"] = false;
```

# Configuration for MongoHQ #
There are two ways to log-in mongodb located on MongoHQ.

## Log-in with MongoHQ account ##
```
$MONGO["servers"][$i]["mongo_name"] = "MongoHQ";
$MONGO["servers"][$i]["mongo_host"] = "flame.local.mongohq.com";
$MONGO["servers"][$i]["mongo_port"] = "27075";
$MONGO["servers"][$i]["mongo_auth"] = true;
$i ++;
```

Then on log-in screen, you should input the username and password, dbname which registered on MongoHQ, then click "log-in".

## Log-in with control account ##
```
$MONGO["servers"][$i]["mongo_host"] = "flame.local.mongohq.com";
$MONGO["servers"][$i]["mongo_port"] = "27075";
$MONGO["servers"][$i]["mongo_user"] = "MongoHQ account";
$MONGO["servers"][$i]["mongo_pass"] = "MongoHQ password";
$MONGO["servers"][$i]["mongo_db"] = "MongoHQ Database Name";
$MONGO["servers"][$i]["mongo_auth"] = false;
$MONGO["servers"][$i]["control_users"]["admin"] = "123456";//control user name  is "admin", password is "123456"
$i ++;
```

Change mongo\_user, mongo\_pass and mongo\_db to yours, then you can log-in with control user name and password (admin/123456 in this example).