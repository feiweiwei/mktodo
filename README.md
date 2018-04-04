# 动手写个小程序－TodoList

## 前言

前两天写过一篇关于我对小程序的看法和对未来前端发展趋势，接触小程序开发也有两周左右了，对于一个之前从来没有正经写过js代码的我来说，并没有遇到多大的麻烦，相对写原生代码和服务端代码要简单很多，也更容易上手，今天这篇就介绍下小程序的基础和如何动手写个Todolist，TodoList也是iOS和android官方入门教程的保留曲目，通过TodoList的编写基本可以初步认识下小程序。
微信为小程序提供了IDE工具，目前的版本更新到了V1.0.2，虽然有时候还存在一些bug不过已经相对比原来好用很多了，具体就不介绍如何使用IDE了，做过开发的同学一看就明白，一个很简单的IDE工具。
下载地址：[微信小程序IDE](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)

## 小程序工程结构
![Screenshot 2018-04-03 13.57.27](http://otxp3yk5p.bkt.clouddn.com/Screenshot 2018-04-03 13.57.27.png)

这是一个小程序工程的目录，从目录结构我们可以看出下面3个app开头的文件是整个工程的一些配置文件:

* app.js: 用于定义小程序的js公共逻辑。
* app.json: 是对当前小程序的公共全局配置，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等。
* app.wxss: wxss用于定义小程序的公共样式，类似于H5中的CSS，连基本语法也是一样的，用于定义页面样式。

上面还有一些文件夹，assets和images是分别用于存放一些大文件和图片的，例如音频、本地文件之类的都可以存在里面，文件夹名称是可以随意更改的，不像android这类资源文件夹是有个规范的约定，不能随便修改名称。
pages文件夹中存放的就是各种页面模块，这里建了两个页面模块，一个是index首页，一个是logs操作日志页，小程序中要求下方tab最少甚至2个，最多设置5个，在使用的时候要注意下。
每个页面模块一般由3类文件组成：

* xxx.js： 在js文件中主要是用来定义页面变量和函数方法的，小程序的定义语法和vue.js这类MVVM框架非常像，可以直接参考最后一节的代码样例，一看就明白了。
* xxx.wxml：wxml类似h5中的html文件，用于描述页面的布局结构，需要注意的是wxml的标签名称和html的还是有很大不同的，需要熟悉下，这些标签和关键字。
* xxx.wxss：wxss类似于css文件，其中描述了页面中需要用到的样式。


## 数据绑定
数据绑定是整个小程序框架的核心，其实就是客户端用的比较多的MVVM框架，可以做到逻辑层的数据和视图层的数据关联变更，这样就可以方便的实现通过事件触发逻辑层的数据变化，从而体现到视图层展示给用户看到的数据变化。以前写过.net、vue.js，用过android、ios MVVM框架的同学是不是都很熟悉这样的data binding模式。


```JavaScript
//在js文件中定义好了数据message
Page({
  data: {
    message: 'Hello MINA!'
  }
})
```
在wxml页面布局文件中定义好了

```html
//在页面布局文件中引用js中定义的message，就可以在页面展示逻辑层定义的数据了，同时逻辑层的message如果修改了，同时框架也会触发页面局部刷新
<view> {{ message }} </view>
```


## 基本语法
一门计算机语言的基本语法无外乎，变量定义、数据类型、基础运算符、基础语句、基础类库这些，下面我们就简单介绍下这些，让有经验的开发人员一看就明白。

#### 变量定义
在js中定义的变量均为值引用，没有声明的变量直接赋值使用会被定义为全局变量，变量定义和javascript一致。


```JavaScript
var num = 1;
var str = "hello world!";
var eof;
```
上面定义变量的方式和javascript是一模一样的，var变量会根据赋值的类型将变量定义为相应的数据类型。


#### 数据类型
小程序支持的数据类型有：
Number ： 数值
String ：字符串
Boolean：布尔值
Object：对象
Function：函数
Array : 数组
Date：日期
Regexp：正则

这些类型和JavaScript中的类型也是一致的，所以对于有一定js基础的同学，学小程序是非常简单的，这些数据类型对应的方法这里就不介绍了。

#### 基础运算符
小程序的基础运算符和常见语言的基础运算符使用方法一模一样，也是一元运算符、二元运算符、三元运算符、比较运算符、等值运算符、赋值运算符、运算符优先级也和js、C、Java这类的语言一样，所以基础运算符这里就不介绍了，看看下面的实例代码就会用了。

#### 基础语句
小程序中的基础语句也和常用语言一样，就是if/else、switch、for、while这些，用法也是和其他主流语言一致，一看就明白了。

```java
if (表达式) {
  代码块;
} else {
  代码块;
}
```

```java
switch (表达式) {
  case 变量:
    语句;
  case 数字:
    语句;
    break;
  case 字符串:
    语句;
  default:
    语句;
}
```

```java
for (语句; 语句; 语句) {
  代码块;
}

```

```java
while (表达式){
  代码块;
}
```

#### 基础类库
每个语言的基础类库一般多少都有一些差别，小程序的基础类库和JavaScript的基础类库基本一致，熟悉ES5或者ES6标准的同学了解下就会使用了。

| 类库名称    | 属性                                       | 方法                                       |
| ------- | ---------------------------------------- | ---------------------------------------- |
| console |                                          | `console.log` 方法用于在 console 窗口输出信息。它可以接受多个参数，将它们的结果连接起来输出。 |
| Math    | `E`  `LN10`  `LN2`  `LOG2E`  `LOG10E`  `PI`  `SQRT1_2`  `SQRT2` | `abs`  `acos`  `asin`  `atan`  `atan2`  `ceil`  `cos`  `exp`  `floor`  `log`  `max`  `min`  `pow`  `random`  `round`  `sin`  `sqrt`  `tan` |
| JSON    |                                          | `stringify(object)`: 将 `object` 对象转换为 `JSON` 字符串，并返回该字符串。  `parse(string)`: 将 `JSON` 字符串转化成对象，并返回该对象。 |
| Number  | `MAX_VALUE`  `MIN_VALUE`  `NEGATIVE_INFINITY`  `POSITIVE_INFINITY` |                                          |
| Date    | `parse`  `UTC`  `now`                    |                                          |
| Global  | `NaN`  `Infinity`  `undefined`           | `parseInt`  `parseFloat`  `isNaN`  `isFinite`  `decodeURI`  `decodeURIComponent`  `encodeURI`  `encodeURIComponent` |
|         |                                          |                                          |





## 常用组件

#### 视图容器

视图容器很好理解，做过原生开发的同学可以理解为类似android中的各种layout，所有的视图组件都要在一个容器中。

| 组件名                                      | 说明      |
| ---------------------------------------- | ------- |
| [view](https://developers.weixin.qq.com/miniprogram/dev/view.html) | 视图容器    |
| [scroll-view](https://developers.weixin.qq.com/miniprogram/dev/scroll-view.html) | 可滚动视图容器 |
| [swiper](https://developers.weixin.qq.com/miniprogram/dev/swiper.html) | 滑块视图容器  |

#### 基础内容

基础内容组件没啥好说的，就是常见的文本框、进度条，这些在原生开发中可能被官方定义为基础视图view组件，而微信官方将这些定义为了基础内容组件。

| 组件名                                      | 说明   |
| ---------------------------------------- | ---- |
| [icon](https://developers.weixin.qq.com/miniprogram/dev/icon.html) | 图标   |
| [text](https://developers.weixin.qq.com/miniprogram/dev/text.html) | 文字   |
| [progress](https://developers.weixin.qq.com/miniprogram/dev/progress.html) | 进度条  |

#### 表单

表单组件沿用了js中的叫法，在原生开发中这些按钮、输入框这些都叫做基础视图组件，小程序中的常用视图组件比android和ios中的少了很多，但是这些基本能够满足日常开发需求了。

| 标签名                                      | 说明      |
| ---------------------------------------- | ------- |
| [button](https://developers.weixin.qq.com/miniprogram/dev/button.html) | 按钮      |
| [form](https://developers.weixin.qq.com/miniprogram/dev/form.html) | 表单      |
| [input](https://developers.weixin.qq.com/miniprogram/dev/input.html) | 输入框     |
| [checkbox](https://developers.weixin.qq.com/miniprogram/dev/checkbox.html) | 多项选择器   |
| [radio](https://developers.weixin.qq.com/miniprogram/dev/radio.html) | 单项选择器   |
| [picker](https://developers.weixin.qq.com/miniprogram/dev/picker.html) | 列表选择器   |
| [picker-view](https://developers.weixin.qq.com/miniprogram/dev/picker-view.html) | 内嵌列表选择器 |
| [slider](https://developers.weixin.qq.com/miniprogram/dev/slider.html) | 滚动选择器   |
| [switch](https://developers.weixin.qq.com/miniprogram/dev/switch.html) | 开关选择器   |
| [label](https://developers.weixin.qq.com/miniprogram/dev/label.html) | 标签      |

#### 导航

小程序中的页面路由都是通过框架进行跳转，其中页面都是通过runtime的页面栈进行管理，具体的页面栈管理可以查看官方对页面栈的说明，这块需要好好学习下，和原生开发中的栈管理还是存在一些区别的，导航组件跳转方式的不同会导致页面对栈的操作不同，同时也会调用页面不同的生命周期回调。

| 组件名                                      | 说明   |
| ---------------------------------------- | ---- |
| [navigator](https://developers.weixin.qq.com/miniprogram/dev/navigator.html) | 应用链接 |

#### 多媒体

多媒体组件就比较好理解了，就是常见的音频、视频、图片展示，小程序已经将基础功能封装好了，使用起来非常方便。

| 组件名                                      | 说明   |
| ---------------------------------------- | ---- |
| [audio](https://developers.weixin.qq.com/miniprogram/dev/audio.html) | 音频   |
| [image](https://developers.weixin.qq.com/miniprogram/dev/image.html) | 图片   |
| [video](https://developers.weixin.qq.com/miniprogram/dev/video.html) | 视频   |

#### 地图

小程序目前也提供了地图组件，小程序的地图组件使用起来个人感觉比百度和高德的sdk要简单。

| 组件名                                      | 说明   |
| ---------------------------------------- | ---- |
| [map](https://developers.weixin.qq.com/miniprogram/dev/map.html) | 地图   |

#### 画布

画布组件个人一直没有用过，这里就不多介绍了，感兴趣的朋友可以自己查看官方文档。

| 组件名                                      | 说明   |
| ---------------------------------------- | ---- |
| [canvas](https://developers.weixin.qq.com/miniprogram/dev/canvas.html) | 画布   |



## 常用API

大家都知道微信小程序最牛逼的地方在于有微信巨大的用户流量和微信原生API的支持，下面就介绍下常用的微信原生API，通过这些原生API可以实现对原生操作系统一些API的操作和微信app自身功能的调用。

目前小程序开放的API能力已经非常丰富了，手机硬件基本都可以操作了，小程序现阶段提供的API包括：

* 网络请求、文件上传、下载、WebSocket相关操作
* 本地图片操作、录音操作、音频操作、视频操作
* 本地文件操作
* 本地缓存操作
* 地理位置操作、地图操作
* 系统基本信息查询
* 加速器、罗盘、电话、蓝牙、NFC、WiFi、iBeacon等操作
* 微信开放平台登录、授权、支付、转发、二维码、卡券、APP跳转、小程序跳转等相关接口


微信为小程序具体开放的接口细节请参考官方文档 https://developers.weixin.qq.com/miniprogram/dev/api/


## TodoList

#### app.json

```json
{
  //定义所有页面的相对路径，框架会自动去相应目录众找到目录同名的wxss、wxml、wxs、js、json的相关文件
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  //定义小程序窗口的字体、背景色、titlebar内容等信息
  "window":{
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "TODOS",
    "navigationBarTextStyle":"black"
  },
  //定义下方tabbar
  "tabBar": {
    "color": "#999",
    "selectedColor": "#222",
    "backgroundColor": "#f8f9fb",
    "borderStyle": "white",
    //通过list接收tab数组，每个数组中需要定义页面目录相对路径、文字、未选中图标、选中图标
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "todos",
        "iconPath": "assets/todos.png",
        "selectedIconPath": "assets/todos-active.png"
      },
      {
        "pagePath": "pages/logs/logs",
        "text": "logs",
        "iconPath": "assets/logs.png",
        "selectedIconPath": "assets/logs-active.png"
      }
    ]
  }
}
```

#### app.wxss

```css
.container {
  padding: 30rpx;
  border-top: 1rpx solid #e5e5e5;
}
```
#### index.wxml

```html
<view class="container">
  <view class="header">
    <image class="plus" src="../../assets/plus.png" bindtap='addTodoHandle'/>
    <input class="new-todo" value="{{ input }}" placeholder="Anything here..." auto-focus bindinput="inputChangeHandle" bindconfirm="addTodoHandle"/>
  </view>
  <!-- 根据任务数判断展示哪段代码块 -->
  <block wx:if="{{ todos.length }}">
    <view class="todos">
      <!--列表展示所有任务 -->
      <view class="item{{ item.completed ? ' completed' : '' }}" wx:for="{{ todos }}" wx:key="{{ index }}" bindtap="toggleTodoHandle" data-index="{{ index }}">
        <!-- 任务状态根据item项是否completed: success, todo: circle，根据状态定义icon type -->
        <icon class="checkbox" type="{{ item.completed ? 'success' : 'circle' }}"/>
        <text class="name">{{ item.name }}</text>
        <icon class="remove" type="clear" size="16" catchtap="removeTodoHandle" data-index="{{ index }}"/>
      </view>
    </view>
    <view class="footer">
      <text class="btn" bindtap="toggleAllHandle">Toggle all</text>
      <text wx:if="{{ leftCount }}">{{ leftCount }} {{ leftCount === 1 ? 'item' : 'items' }} left</text>
      <text class="btn" wx:if="{{ todos.length > leftCount }}" bindtap="clearCompletedHandle">Clear completed</text>
    </view>
  </block>
  <block wx:else>
    <view class="empty">
      <text class="title">Congratulations!</text>
      <text class="content">There's no more work left.</text>
    </view>
  </block>
</view>

```
#### index.wxss

```css
.header {
  display: flex;
  align-items: center;
  border: 1rpx solid #e0e0e0;
  border-radius: 10rpx;
  box-shadow: 0 0 5rpx #e0e0e0;
  margin-bottom: 30rpx;
  padding: 20rpx;
}

.header .plus {
  width: 41rpx;
  height: 41rpx;
  margin-right: 20rpx;
}

.header .new-todo {
  flex: 1;
  font-size: 28rpx;
}

.todos {
  border: 1rpx solid #e0e0e0;
  border-radius: 10rpx;
  box-shadow: 0 0 5rpx #e0e0e0;
}

.todos .item {
  display: flex;
  align-items: center;
  padding: 25rpx;
  border-bottom: 1rpx solid #e0e0e0;
}

.todos .item:last-child {
  border-bottom: 0;
}

.todos .item .checkbox {
  margin-right: 20rpx;
}

.todos .item .name {
  flex: 1;
  font-size: 30rpx;
  color: #444;
}

.todos .item.completed .name {
  text-decoration: line-through;
  color: #888;
}
/* 
.todos .item .remove {
  cursor: pointer;
}
*/
.footer {
  display: flex;
  justify-content: space-between;
  margin: 30rpx 0;
  padding: 0 10rpx;
  font-size: 26rpx;
  color: #777;
}
/* 
.footer .btn {
  cursor: pointer;
}
*/
.empty {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.empty .title {
  font-size: 60rpx;
  margin: 200rpx 50rpx 50rpx;
  color: #444;
}

.empty .content {
  color: #666;
  text-align: center;
}

```

#### index.js

```JavaScript
Page({
  //定义页面变量
  data: {
    input: '',
    todos: [],
    leftCount: 0,
    allCompleted: false,
    logs: []
  },
//保存方法，将todo-list和todo-logs保存在小程序本地，通过调用小程序开放api wx.setStorageSync（）
  save: function () {
    wx.setStorageSync('todo_list', this.data.todos)
    wx.setStorageSync('todo_logs', this.data.logs)
  },
//加载本地缓存中的todo-list
  load: function () {
    var todos = wx.getStorageSync('todo_list')
    if (todos) {
      var leftCount = todos.filter(function (item) {
        return !item.completed
      }).length
      this.setData({ todos: todos, leftCount: leftCount })
    }
    var logs = wx.getStorageSync('todo_logs')
    if (logs) {
      this.setData({ logs: logs })
    }
  },

  onLoad: function () {
    this.load()
  },

  inputChangeHandle: function (e) {
    this.setData({ input: e.detail.value })
  },
//增加任务
  addTodoHandle: function (e) {
    if (!this.data.input || !this.data.input.trim()) return
    var todos = this.data.todos
    //将任务数据push到map中
    todos.push({ name: this.data.input, completed: false })
    var logs = this.data.logs
    logs.push({ timestamp: new Date(), action: 'Add', name: this.data.input })
    this.setData({
      input: '',
      todos: todos,
      leftCount: this.data.leftCount + 1,
      logs: logs
    })
    this.save()
  },
//完成任务
  toggleTodoHandle: function (e) {
    var index = e.currentTarget.dataset.index
    var todos = this.data.todos
    todos[index].completed = !todos[index].completed
    var logs = this.data.logs
    logs.push({
      timestamp: new Date(),
      action: todos[index].completed ? 'Finish' : 'Restart',
      name: todos[index].name
    })
    this.setData({
      todos: todos,
      leftCount: this.data.leftCount + (todos[index].completed ? -1 : 1),
      logs: logs
    })
    this.save()
  },
//移除所有任务
  removeTodoHandle: function (e) {
    var index = e.currentTarget.dataset.index
    var todos = this.data.todos
    var remove = todos.splice(index, 1)[0]
    var logs = this.data.logs
    logs.push({ timestamp: new Date(), action: 'Remove', name: remove.name })
    this.setData({
      todos: todos,
      leftCount: this.data.leftCount - (remove.completed ? 0 : 1),
      logs: logs
    })
    this.save()
  },

  toggleAllHandle: function (e) {
    this.data.allCompleted = !this.data.allCompleted
    var todos = this.data.todos
    for (var i = todos.length - 1; i >= 0; i--) {
      todos[i].completed = this.data.allCompleted
    }
    var logs = this.data.logs
    logs.push({
      timestamp: new Date(),
      action: this.data.allCompleted ? 'Finish' : 'Restart',
      name: 'All todos'
    })
    this.setData({
      todos: todos,
      leftCount: this.data.allCompleted ? 0 : todos.length,
      logs: logs
    })
    this.save()
  },
  
  clearCompletedHandle: function (e) {
    var todos = this.data.todos
    var remains = []
    for (var i = 0; i < todos.length; i++) {
      todos[i].completed || remains.push(todos[i])
    }
    var logs = this.data.logs
    logs.push({
      timestamp: new Date(),
      action: 'Clear',
      name: 'Completed todo'
    })
    this.setData({ todos: remains, logs: logs })
    this.save()
  }
})


```



## 总结

TodoList这个例子其实很简单，大家看着注释就能知道什么意思了。这篇文章其实主要目的还是让大家小程序入门，对于有一定其他语言开发经验的同学应该看这一篇基本就入门了，后续会再补充几篇小程序开发进阶的文章，会涉及到一些小程序网络请求、页面生命周期、微信API的使用、runtime的一些内容，敬请期待。
