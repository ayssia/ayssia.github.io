# 雀魂 Ex

## 免责声明

在您使用`雀魂Ex`进行游戏时造成的`包含但不局限于限制登录、封号等`后果`均由用户自行承担`, `雀魂Ex`不对此承担任何责任!

## 开发

### 开发进度

- iOS: `3.1.6 正式版`
- Android: `1.1.2 正式版`

## 安装

### 安卓

点击 `==>` [下载安卓版本](https://github.com/moxcomic/majsoul-ex/releases/download/iOS%2FAndroid/majsoulex_android_1.1.2.apk) `<==`

### iOS

点击 `==>` [下载 iOS 版本](https://github.com/moxcomic/majsoul-ex/releases/download/iOS%2FAndroid/majsoulex_ios_3.1.6.ipa) `<==`

#### 注意事项

iOS 由于系统原因`不能直接使用iPhone/iPad下载安装`, 需要使用签名方式安装, 具体方式请自行百度

### 雀魂麻将助手

- ver: 0.0.16  
  点击 `==>` [下载 macOS 版本](https://github.com/moxcomic/majsoul-ex/releases/download/majsoul_helper/majsoulex_helper_mac) `<==`  
  点击 `==>` [下载 Windows 版本](https://github.com/moxcomic/majsoul-ex/releases/download/majsoul_helper/majsoulex_helper_win64.exe) `<==`  
  该工具是在[日本麻将助手](https://github.com/EndlessCheng/mahjong-helper)的基础上进行的扩展，具体功能请访问原作者页面。  
  GUI `==>` [GUI 项目地址](https://github.com/moxcomic/majsoulex_gui)

### 其他

- [雀 Ex 项目地址](https://github.com/moxcomic/majsoul-ex)
- [最新发布版本](https://github.com/moxcomic/majsoul-ex/releases/tag/iOS%2FAndroid)

## 新增功能/修改雀魂原功能

- 复制友人房链接、雀口令后会弹窗提示是否加入房间, 点击确定后一键加入
  - 该功能需要登录到游戏主页面才会弹窗
- 复制牌谱链接后会弹窗提示是否查看牌谱, 点击确定后一键进入牌谱
  - 该功能需要登录到游戏主页面才会弹窗
- 友人房链接`复制链接`功能修改
- 牌谱`分享`功能修改

### 雀口令

雀口令是在雀魂友人房链接上发展出来的新型分享链接方式, 可以自定义更多的分享内容

#### 雀口令支持变量列表

- \[token\]: 雀口令本体
- \[roomid\]: 房间号
- \[roomlink\]: 雀魂友人房原链接内容
- \[maxplayer_d\]: 房间最大人数, 阿拉伯数字 3/4
- \[maxplayer_s\]: 房间最大人数, 大写 三/四
- \[roommode\]: 房间模式, 东/南

### 快捷指令

为了支持`雀魂Plus`雀 Ex 在`快捷指令`部分内容使用雀魂 Plus 的配置, 两者可通用。  
在`雀Ex`初始化时会出入`Majsoul_Plus`字段, 之后`每个插件被载入前`会在前面的字段中注册`以插件ID为字段的Key`, 之后只要`在JS中`使用`Majsoul_Plus["id"] = xxx`注册即可, 详细可参考`我全都要`插件的写法。

```
if (!window.wqdy) {
    window.wqdy = new WQDY();
    window.wqdy.readSetting();
    Majsoul_Plus["wqdy"] = {
        name: "我全都要",
        actions: {
            "手动保存配置": () => window.wqdy.writeSetting(),
            "切换表情显示": () => {
                args.isUseOriginEmoji = !args.isUseOriginEmoji;
                localStorage.setItem("isUseOriginEmoji", args.isUseOriginEmoji);
                return "应用成功，下一局游戏生效。"
            },
            "按性别排序角色": () => {
                args.isSexSort = !args.isSexSort;
                localStorage.setItem("isSexSort", isSexSort);
                return "应用成功，重新启动游戏后生效。"
            }
        }
    }
    console.log("我全都要 加载完毕");
} else {
    console.warn("")
}
```

## 制作扩展

### 图片资源替换部分

1. 直接替换`/Android/data/com.yuuki.majsoulex/files/Cache`路径下的图片文件
2. 制作图片资源替换扩展

### 制作图片资源替换扩展

#### 目录格式

```
- 插件名称文件夹
  // 该文件负责描述该扩展的所有信息
  - extension.json
  // 资源存放文件夹, 所有需要替换的资源必须存放于此路径下
  - assets
    - 文件夹
      - 图片.png
    - 图片.png
```

下面给出一个`extension.json`的例子

```
{
  "id": "id",
  "version": "1.0.0",
  "name": "name",
  "author": "author",
  "description": "description",
  "preview": "preview.png",

  "replace": [
    // 直接替换包含该路径的图片为assets文件下同路径文件
    "audio/sound/zeniya/fan_dora10.mp3",
    "scene/Assets/Resource/mjpai/en/mjp_default_0/8p.png",
    // 替换from路径的文件为assets路径下的to文件
    {
      "from": "audio/sound/qianzhi/lobby_normal1.mp3",
      "to": "audio/quack.mp3"
    }
  ]
}
```

制作完成后将第一步插件文件夹名称直接生成压缩包即可被雀魂 Ex 识别

### JavaScript 扩展制作

`待更新...`

## 制作扩展源

### GitHub 部署部分

1. 部署一个 Github Pages
2. 添加一个`src.ex`文件

### src.ex

下面给出雀魂 Ex 的`src.ex`部分代码展示

```
{
    // 扩展源信息
    "info":
    {
        "id": "com.moxcomic.MajsoulEx",
        "name": "雀魂Ex官方源",
        "author": "MajsoulEx",
        "email": "656469762@qq.com",
        "description": "雀魂Ex官方源, 由「雀魂X」、「雀魂Ex」开发者维护更新, 本源仅收录插件并不开发插件, 需要投稿插件请添加QQ 656469762, 如果收录的插件侵犯了您的权益请联系我们, 在我们确认所有权后会对本源上的侵权插件进行下架",
        "icon": "https://raw.githubusercontent.com/moxcomic/moxcomic.github.io/master/icon.png"
    },
    // 扩展源发布扩展
    "release":
    [
        {
            "id": "RetinalCanvas",
            "name": "全面屏适配",
            "description": "先通过修改舞台尺寸实现视网膜画布，再通过修改界面去除黑边。\n支持拉伸来实时改变分辨率",
            "author": "88826",
            "version": "1.3.0",
            "preview": "preview.jpg",
            // 该扩展所在的仓库
            "homepage": "https://github.com/moxcomic/RetinalCanvas.git"
        }
    ]
}
```

### 仓库下载方式

下面为一个例子

```
// 如果不填写此项则默认为Archive方式下载
"source":
{
    // 扩展的发布方式
    "type": "release",
    // 扩展的Tag字段, 用于Release模式指定Tag
    "tag": "2.0.0",
    // 扩展文件名, 用于Release/Http/Raw下载模式指定下载文件名
    "file": "mjpai_BiliBiliTV.mspr"
}
```

### Archive 方式

```
假设插件的`版本`为`1.0.0`
git add .
git git commit -m "update"
git push origin master
git tag 1.0.0
git push --tags
```

### Release 方式

```
git add .
git git commit -m "update"
git push origin master
手动在Github打Release包上传文件
Tag和File即为你手动填写的值
```

### Http 方式

```
手动上传至任意地方, 此模式必须使用可以直接下载的直链
```

### Raw 方式

```
将插件文件(.ex/.mspe/.mspm/.mspr)直接上传至仓库, 并填写file为该文件名即可
```

## 联系方式

- B 站 ID: [神崎·H·亚里亚](https://space.bilibili.com/898411/)
- B 站 ID: [关野萝可](https://space.bilibili.com/612462792/)
- QQ 交流群: [991568358](https://jq.qq.com/?_wv=1027&k=3gaKRwqg)
- Twitter: @MajsoulEx

## 赞助

如果对您有所帮助，欢迎您的赞赏

<figure class="third">
    <img src="https://moxcomic.github.io/wechat.png" width=300>
    <img src="https://moxcomic.github.io/alipay.png" width=300>
    <img src="https://moxcomic.github.io/qq.png" width=300>
</figure>
