创建 插件流程

定义
``` batch
plugin_id		= com-example-myplugins
plugin_name		= MyPlugins
class 			= com.example.MyPlugins
#android 插件拷贝路径
android-target-dir 	= src/com/example/
```

创建插件
```
plugman create --name plugin_name --plugin_id plugin_id --plugin_version 0.0.1
```

添加支持android
```
plugman platform add --platform_name android
```

修改
plugin.xml
``` xml
<?xml version="1.0" encoding="utf-8"?>
<plugin	xmlns="http://apache.org/cordova/ns/plugins/1.0" 
	xmlns:android="http://schemas.android.com/apk/res/android" 
	id="${plugin_id}" 
	version="0.0.1"	>  
  <name>${plugin_name}</name>  
  <js-module name="${plugin_name}" src="www/${plugin_name}.js"> 
    <clobbers target="cordova.plugins.${plugin_name}"/> 
  </js-module>
  <platform name="android">
    <config-file parent="/*" target="res/xml/config.xml">
      <feature name="${plugin_name}">
        <param name="android-package" value="${class}"/>
      </feature>
    </config-file>
    <config-file parent="/*" target="AndroidManifest.xml"/>
        <source-file src="src/android/${plugin_name}.java" target-dir="${android-target-dir}" />
  </platform> 
</plugin>
```

添加
package.json
``` json 
{
  "name": "${plugin_name}",
  "version": "1.0.0",
  "description": "${plugin_name}",
  "cordova": {
    "id": "${plugin_id}",
    "platforms": [
      "android"
    ]
  },
  "author": "",
  "license": "ISC"
}
```

添加到项目
```
cordova plugin add D:\project\android\dsej\cordova-plugins\MyPlugins
```

