[&#8249; YouTube Doc Home](./)

<h1>YouTube 集成指南</h1>
<<[../../shared/-VERSION-/version.md]

## 集成
在您确保正确安装了 SDKBOX installer 的情况下，运行下面的命令来集成 SDKBOX Youtube 插件。
```bash
$ sdkbox import youtube
```

<<[../../shared/notice.md]

<!--## Configuration
<<[../../shared/sdkbox_cloud.md]
<<[../../shared/remote_application_config.md]-->


### JSON 配置
SDKBOX Installer 将会自动在您的 `sdkbox_config.json` 中插入一份配置样例。请修改这份配置样例，使其能用于您自己的 app 。

如果您想在您的 app 中显示 Youtube 视频， 您需要在 [这里](https://developers.google.com/youtube/android/player/register#Create_API_Keys) 注册一个新的 Youtube 的 API KEY。并把它加入 `sdkbox_config.json` 文件的 `developer_key` 字段中。

#### iOS 可选配置

- "show_close_button": [bool] 是否显示关闭按钮

- "close_button_text": [string] 设置关闭按钮文字，默认 "X"，不能和 "close_button_image" 同时使用

- "close_button_image": [string] 设置关闭按钮图片, 不能和 "close_button_text" 同时使用

```json
{
    "ios" :
    {
        "Youtube":
        {
            "developer_key":"AIzaSyDMuDjrVSL3uj_QvlI3bbjKn5I4nNB1XZk"
        }
    },
    "android" :
    {
        "Youtube":
        {
            "developer_key":"AIzaSyDMuDjrVSL3uj_QvlI3bbjKn5I4nNB1XZk"
        }
    }
}
```

## 使用
<<[usage.md]

<<[api-reference.md]

<<[manual_integration.md]

<<[manual_ios.md]

<<[../../shared/manual_integration_android_and_android_studio.md]

<<[manual_android.md]

<<[extra-step.md]

<<[proguard.md]
