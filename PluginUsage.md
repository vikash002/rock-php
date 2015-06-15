

[Plugin](Plugin.md) > For Users

## How to install plug-in? ##

When you want to install a plug-in, just download it and extract files to plugins directory:
```
  app/
     plugins/
       plugin1/
       plugin2/
       YOUR_PLUGIN_NAME/
       ...
```

Then, we need to enable the plugin in app/configs/rplugin.php:
```
$plugins["YOUR_PLUGIN_NAME"]["enabled"] = 1;
...
```

Replace "YOUR\_PLUGIN\_NAME" to what the plug-in named, and save the file to the disk.

Now, everything will goes well.