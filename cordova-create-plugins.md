## 创建 插件流程

### 首先设定一些参数
``` batch
#插件ID
plugin_id		= com-example-myplugins
#插件名称
plugin_name		= MyPlugins
#android 对应的class
class 			= com.example.MyPlugins
#拷贝到android工程目标路径
android-target-dir 	= src/com/example/
```

### 创建插件（根据设定替换 plugin_name 、plugin_id ）
```
plugman create --name plugin_name --plugin_id plugin_id --plugin_version 0.0.1
```

### 进入插件目录,添加android支持
```
plugman platform add --platform_name android
```

### 修改 plugin.xml（根据设定替换 ${plugin_id}、${plugin_name} 、${class} 、{android-target-dir}）
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

### 添加 package.json（根据设定替换 ${plugin_id}、${plugin_name} ）
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

### 回到cordova根目录添加自定义控件
```
cordova plugin add D:\project\android\dsej\cordova-plugins\MyPlugins
```

