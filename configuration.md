
# Where to change? #

Open _config.php_ under RockMongo installation directory, with your editor (such as notepad) or VI/VIM on Unix/Linux, every configuration options are placed there.

# Authentication #

## mongo\_auth vs control\_auth ##
Once you begin to use RockMongo, you should decide which authentication method to use.

If mongo\_auth set to true, users must log-in on UI interface with their username and password given in MongoDB (added by db.addUser()). So, mongo\_user, mongo\_pass and mongo\_db in configuration will be unavailable now.

If control\_auth set to true and mongo\_auth set to false, users must log-in with control\_users option, mongo\_user, mongo\_pass and mongo\_db will be used if they present in configuration. For security reason, you should always change the default control username and password to a complex one.

If all of them are set to false, users will log-in without any username and password needed.

### mongo\_auth Demo ###
You log-in the system with username, password and dbname from MongoDB.

```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
$MONGO["servers"][$i]["mongo_port"] = "27017";
$MONGO["servers"][$i]["mongo_timeout"] = 0;
$MONGO["servers"][$i]["mongo_auth"] = true;//enable mongo authentication
$i ++;
```

### control\_auth Demo ###
You log-in the system with control username and password.

```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
$MONGO["servers"][$i]["mongo_port"] = "27017";
$MONGO["servers"][$i]["mongo_timeout"] = 0;
//$MONGO["servers"][$i]["mongo_db"] = "MONGO_DATABASE";
//$MONGO["servers"][$i]["mongo_user"] = "MONGO_USERNAME"
//$MONGO["servers"][$i]["mongo_pass"] = "MONGO_PASSWORD";
$MONGO["servers"][$i]["mongo_auth"] = false;//disable mongo authentication

$MONGO["servers"][$i]["control_auth"] = true;//enable control authentication
$MONGO["servers"][$i]["control_users"]["admin"] = "admin";
$MONGO["servers"][$i]["control_users"]["iwind"] = "123456";//more admins go below
$i ++;
```

### no authentication Demo ###
You log-in the system without any username and password.

```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
$MONGO["servers"][$i]["mongo_port"] = "27017";
$MONGO["servers"][$i]["mongo_timeout"] = 0;
//$MONGO["servers"][$i]["mongo_db"] = "MONGO_DATABASE";
//$MONGO["servers"][$i]["mongo_user"] = "MONGO_USERNAME"
//$MONGO["servers"][$i]["mongo_pass"] = "MONGO_PASSWORD";
$MONGO["servers"][$i]["mongo_auth"] = false;//disable mongo authentication

$MONGO["servers"][$i]["control_auth"] = false;//disable control authentication
$i ++;
```

# Mongo #

## mongo\_name ##
v1.1. mongo server name
```
$MONGO["servers"][$i]["mongo_name"] = "Localhost";
```

## mongo\_host ##
v1.1. mongo host
```
$MONGO["servers"][$i]["mongo_host"] = "127.0.0.1";
```

## mongo\_port ##
v1.1. mongo\_port
```
$MONGO["servers"][$i]["mongo_port"] = "27017";
```

## mongo\_db ##
v1.1. default mongo db name to connect, works only if mongo\_auth=false
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
$MONGO["servers"][$i]["mongo_timeout"] = 30;
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