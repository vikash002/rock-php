

[Plugin](Plugin.md) > For Developers

## How plug-in works ##

RockMongo plug-in feature allow you to filter data and listen events.

You registered data filters and event listeners in your plug-in, then RockMongo call them in a proper time.

You also can write controllers in your plug-in, so you can add more operation buttons to server/db/collection/document, users click button then go to your controllers.

You may enable and disable plug-ins in app/configs/rplugin.php.

## Write a plug-in ##

There is only four steps to write a plug-in for RockMongo:
  1. create a plug-in directory under app/plugins
  1. put a init.php in the directory we created
  1. call api to add data filters and event listeners in init.php
  1. enable your plug-in in app/configs/rplugin.php

For instance, you want to create a plug-in named myplugin, so your directory structure will look like this:
```
   app/
      plugins/ 
         myplugin/
             init.php
```

init.php:
```
<?php

function my_filter($data) {
  //filter data
}

RFilter::add("SUPPORTED FILTER NAME", "my_filter");

?>
```

rplugin.php:
```
<?php

$plugins["myplugin"]["enabled"] = 1;
//$plugins["myplugin2"]["enabled"] = 1;
//$plugins["myplugin3"]["enabled"] = 1;

?>
```

## API ##
  * RFilter::add($dataType, $filter, $priority = -1) - add a filter
  * RFilter::remove($dataType, $filter) - remove a filter
  * RFilter::stop($dataType) - stop a filter chain
  * REvent::listen($event, $callback, $priority = -1) - add a event listener
  * REvent::remove($event, $callback)  - remove a event listener
  * REvent::stop($event) - stop event propagation



## Filters ##
### CONFIG\_FILTER ###
Filter RockMongo configuration.

  * Params:
    * array $MONGO global $MONGO variable
  * Demo:
```
function my_config_filter($MONGO) {
	$MONGO["servers"][0]["mongo_name"] = "TestServer";
        //other configurations go below
}
RFilter::add("CONFIG_FILTER", "my_config_filter");
```

### SERVER\_FILTER ###
filter server before authentication, give you a chance to integrate authentication with your own system.
  * Params:
    * MServer $server the server which current user want to log-in
  * Demo:
```
function my_login_filter (MServer $server) {
    $user = $_COOKIE["user"];//suppose you store user name in cookie
    
    //connect to your MySQL or other system to decide which mongo host to log-in

    //set mongo parameters
    $server->setMongoHost("192.168.1.100");
    $server->setMongoPort(27017);
    $server->setMongoUser("...");
    $server->setMongoPass("...");
    $server->setMongoDb("..."); 

    //let the user log-in in without internal authentication filter
    $server->setControlAuth(false);
    $server->setMongoAuth(false);

    //now user log-in with your own authentication
}
RFilter::add("SERVER_FILTER", "my_login_filter");
```


### SERVER\_MENU\_FILTER ###
Add or remove server menu items.
  * Params:
    * array $items menu items
  * Demo:
```
function my_server_menu_filter ($items) {
	$items[] = array( 
		"action" => ("@test.index.index"),
		"name" => "My Menu"
	);
}

RFilter::add("SERVER_MENU_FILTER", "my_server_menu_filter");
```

### DB\_MENU\_FILTER ###
Add or remove database menu items.
  * Params:
    * array $items menu items
    * string $dbName database name
  * Demo:
```
function my_db_menu_filter ($items, $dbName) {
	$items[] = array(
		"action" => "@test.index.db",
		"params" => array ("db" => $dbName), 
		"name" => "My Menu"
	);
}

RFilter::add("DB_MENU_FILTER", "my_db_menu_filter");
```

### COLLECTION\_MENU\_FILTER ###
Add or remove collection menu items.
  * Params:
    * array $items menu items
    * string $dbName database name
    * string $collectionName collection name
  * Demo:
```
function my_collection_menu_filter ($items, $dbName, $collectionName) {
	$items[] = array(
		"action" => "@test.index.collection",
		"params" => array( "db" => $dbName, "collection" => $collectionName ),
		"name" => "My Menu"
	);
}

RFilter::add("COLLECTION_MENU_FILTER", "my_collection_menu_filter");
```

### DOC\_MENU\_FILTER ###
Add or remove document menu items.
  * Params:
    * array $items menu items
    * string $dbName database name
    * string $collectionName collection name
    * mixed $docId document id (use rock\_real\_id($docId) to convert it to real id)
    * integer $docIndex document index
  * Demo:
```
function my_doc_menu_filter ($items, $dbName, $collectionName, $docId, $docIndex) {
	$items[] = array(
		"action" => "@test.index.doc",
		"params" => array( "db" => $dbName, "collection" => $collectionName, "docId" => ($docId), "docIndex" => $docIndex ),
		"name" => "My Menu"
	);
	$items[] = array(
		"action" => "@test.index.doc",
		"params" => array( "db" => $dbName, "collection" => $collectionName, "docId" => ($docId), "docIndex" => $docIndex ),
		"name" => "My Menu2"
	);
}

RFilter::add("DOC_MENU_FILTER", "my_doc_menu_filter");
```

## Events ##

### RENDER\_PAGE\_HEADER\_EVENT ###
Fired when render page header.

Demo:
```
function my_header_event() {
   echo "<link rel=\"stylesheet\" href=\"/css/my.css\" />\n";//add my own stylesheets
}

REvent::listen("RENDER_PAGE_HEADER_EVENT", "my_header_event");
```

### RENDER\_PAGE\_FOOTER\_EVENT ###
Fired when render page footer.

## Controllers in Plug-in ##

You may write your own controllers in plug-in, just make the folders look like this:
```
   plugins/
     YOUR_PLUGIN_NAME/
         init.php
         controllers/
            index.php
            db.php
            MORE CONTROLLERS GO HERE
         views/
            index/ 
               about.php
            db/
               index.php
            MORE VIEWS GO HERE
```

Visit your actions in controller by adding "@" to action name in url:
```
http://MY_HOST/index.php?action=@YOUR_PLUGIN_NAME.CONTROLLER_NAME.ACTION_NAME
http://MY_HOST/index.php?action=@my_plugin.index.about
http://MY_HOST/index.php?action=@my_plugin.db.remove
```

Your controller should always inherit from BaseController class:
```
<?php

import("classes.BaseController");

class IndexController extends BaseController {
    public function doAbout() {
         //action codes here ...
    }
}

?>
```