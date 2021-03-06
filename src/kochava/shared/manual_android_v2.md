## Android 平台手动集成

### 拷贝文件
从插件安装包中的 `plugin/android/libs` 目录拷贝下列 __jar__ 文件到您的工程的 __proj.android/libs__ 目录。

> KochavaSDK.jar

> PluginKochava.jar

> sdkbox.jar

从 `plugin/android/jni` 目录拷贝 `pluginkochava` 以及 `sdkbox` 目录到您的工程的 `proj.android/jni` 目录。如果 `sdkbox` 目录在工程中已经存在，请覆盖它。

### 编辑 `AndroidManifest.xml`
在标签 __application tag__ 上添加下列权限：
```xml
<uses-permission android:name ="android.permission.INTERNET"/>
<uses-permission android:name ="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name ="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name ="android.permission.READ_PHONE_STATE"/>
```

另外，您需要在 __application tag__ 里添加 Kochava 广播接收器以及下面的元数据标签，这些都是 Google Play 数据捕获所需要的。
```xml
<receiver android:name ="com.kochava.android.tracker.ReferralCapture"
  android:exported ="true" >
  <intent-filter>
  <action android:name ="com.android.vending.INSTALL_REFERRER" />
  </intent-filter>
  </receiver>
  <meta-data
    android:name ="com.google.android.gms.version"
    android:value ="@integer/google_play_services_version"/>
```

使 __hardware acceleration__ 属性生效。这一标签是一个在新版本 sdk 上的选项，不能用于2.3.3版本。
```xml
<android:hardwareAccelerated="true" />
```

### 编辑 `Android.mk`
编辑 `proj.android/jni/Android.mk`：

为 __LOCAL_STATIC_LIBRARIES__ 添加额外的库：
```
LOCAL_STATIC_LIBRARIES += android_native_app_glue
LOCAL_LDLIBS += -landroid
LOCAL_LDLIBS += -llog
LOCAL_STATIC_LIBRARIES += PluginKochava
LOCAL_STATIC_LIBRARIES += sdkbox
```

在所有 __import-module__ 语句之前添加一条 call 语句：
```
$(call import-add-path,$(LOCAL_PATH))
```

在最后添加额外的 __import-module__ 语句：
```
$(call import-module, ./sdkbox)
$(call import-module, ./pluginkochava)
```

这意味着您的语句顺序看起来像是这样：
```
$(call import-add-path,$(LOCAL_PATH))
$(call import-module, ./sdkbox)
$(call import-module, ./pluginkochava)
```

### 编辑 `Application.mk`
编辑 `proj.android/jni/Application.mk`：

为 __APP_PATFORM__ 添加版本：
```
APP_PLATFORM := android-9
```
