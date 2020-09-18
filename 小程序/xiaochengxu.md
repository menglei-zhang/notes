## JSON 是一种数据格式，并不是编程语言，在小程序中，JSON扮演的静态配置的角色。

### .json  .wxml  .wxss .js
app.json 是当前小程序的全局配置

view button text  {{ }} bindtab

<view>{{ msg }}</view>
<text>{{ msg }}</text>
<button bindtap="clickMe">点击我</button>

clickMe() {
    this.setData({ msg: "Hello World!"})
}

## 渲染层 和 逻辑层
小程序的运行环境分为渲染层和逻辑层
WXML 和 WXSS 为渲染层
JS 为工作逻辑层

小程序的渲染层和逻辑层分别由2个线程管理：渲染层的界面使用了WebView 进行渲染；逻辑层采用JsCore线程运行JS脚本。
一个小程序存在多个界面，所以渲染层存在多个WebView线程
