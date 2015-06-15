

# Installation #

## How to quickly start with `RockMongo`? ##
If you are working on Windows or Mac OS X, there are [softwares](RelatedProjects.md) can help you quickly start with RockMongo, without installing PHP manually.

[ParmaStack](https://github.com/synthomat/ParmaStack/downloads) also includes a Unix version, you can check out it and have a try.

# Configuration #

## How to disable authentication? ##

set mongo\_auth and control\_auth to false:
```
$MONGO["servers"][$i]["mongo_auth"] = false;
...
$MONGO["servers"][$i]["control_auth"] = false;
```


## How to connect MongoHQ ##

See configuration for MongoHQ here: http://code.google.com/p/rock-php/wiki/configuration#Configuration_for_MongoHQ

## How to change password ##
See configuration for Authenticate: http://code.google.com/p/rock-php/wiki/configuration?ts=1336443212&updated=configuration#control_users

Basically, open _config.php_, and add lines below to right position:
```
$MONGO["servers"][$i]["control_users"]["myusername"] = "mypassword";
$MONGO["servers"][$i]["control_users"]["iwind"] = "123456";
```


# Known issues #

## How to fix 500/502 errors? ##

Basically, it was caused by php\_mongo.so (or php\_mongo.dll on windows), you should upgrade your php\_mongo driver from http://pecl.php.net/package/mongo or download a latest dll from http://us.php.net/manual/en/mongo.installation.php#mongo.installation.windows.

After new driver installation, restart your web server, and refresh the RockMongo, it will goes ok. Otherwise, you should send us php error log so that we can analyze the reason.

## PHP Error: Fatal error: Allowed memory size when export a large DB ##

To export a large db, you need to change your configures in your php.ini :

```
max_execution_time = 30
memory_limit = 128M
```

to larger numbers, such as:

```
max_execution_time = 1200
memory_limit = 1024M
```

Then you need to restart your web server (apache, fastcgi ....).