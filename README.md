# **      神奇甲骨主要知识点**

1.[uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/case.html)

## CSS 支持

[CSS 支持 | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/tutorial/syntax-css.html)

**如何运行**

[uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/quickstart-hx.html#运行uni-app)

**打包**

[uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/quickstart-hx.html#发布uni-app)

# [#](https://uniapp.dcloud.net.cn/tutorial/build/SafePack.html#安心打包使用指南)安心打包使用指南



**页面简介**

[页面简介 | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/tutorial/page.html)

**页面生命周期**

```
函数名	          说明	              	               
onInit	监听页面初始化，其参数同 onLoad 参数，为上个页面传递的数据，参数类型为 Object（用于页面传参），触发时机早于 onLoad	
onLoad	监听页面加载，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参），参考示例		
onShow	监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面		
onReady	监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发		
onHide	监听页面隐藏		
onUnload	监听页面卸载	
```



一个uni-app工程，默认包含如下目录及文件：<u></u>

```
┌─uniCloud              云空间目录，阿里云为uniCloud-aliyun,腾讯云为uniCloud-tcb（详见uniCloud）
│─components            符合vue组件规范的uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─utssdk                存放uts文件
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用的本地静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─uni_modules           存放[uni_module](/uni_modules)。
├─platforms             存放各平台专用页面的目录，详见
├─nativeplugins         App原生语言插件 详见
├─nativeResources       App端原生资源目录
│  └─android            Android原生资源目录 详见
├─hybrid                App端存放本地html文件的目录，详见
├─wxcomponents          存放小程序组件的目录，详见
├─unpackage             非工程代码，一般存放运行或发行的编译结果
├─AndroidManifest.xml   Android原生应用清单文件 详见
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 应用生命周期
├─manifest.json         配置应用名称、appid、logo、版本等打包信息，详见
├─pages.json            配置页面路由、导航条、选项卡等页面类信息，详见
└─uni.scss              这里是uni-app内置的常用样式变量
	
```

<template>
	<view class="page_edu">
		<view class="page_edu_header">
			<view class="header">
				<image src="/static/icon_main.png" class="btn"></image>
				<view class="input">
					<image src="/static/search.png" class="search"></image>
					<input type="text" value="" placeholder="搜索" />
				</view>
				<image src="/static/msg.png" class="btn"></image>
			</view>
			<view class="header_content">
				<view class="left">
					<text class="title">神奇甲骨</text>
					<text class="sub_title">重视甲骨文的历史文化价值，加强汉字基本功和书法技巧的学习</text>
					<!-- <text class="btn">免费试学</text> -->
				</view>


				<view>
					<image src="/static/right.png" style="width: 131px;height: 122px;"></image>
				</view>
			</view>
		</view>
		<view class="page_content">
			<view class="menu">
				<template v-for="(it,i) in menus">
					<view class="item" :key="'menu_'+i" @tap="navigateTo(it.menus_type)">
						<view class="img_view" :style="{background: it.bg}">
							<image :src="it.icon" class="image"></image>
						</view>
						<text class="txt">{{it.txt}}</text>
					</view>
				</template>
			</view>
			<view class="menu">
				<template v-for="(it,i) in second_menus">
					<view class="item" :key="'s_menu_'+i" @tap="navigateTo(it.menus_type)">
						<!-- <image :src="it.icon" class="image"></image> -->
						<view class="img_view" :style="{background: it.bg}">
							<image :src="it.icon" class="image"></image>
						</view>
						<text class="txt">{{it.txt}}</text>
					</view>
				</template>
			</view>
			<view class="ad">
				<view class="ad_btn">
					<text class="title">甲骨文书法练习课上线</text>
					<!-- <text class="sub_title">老用户现实立减100元</text> -->
				</view>
				<image src="/static/tag.png" class="bg"></image>
			</view>
		</view>
		<scroll-view scroll-x="true" class="slider">
			<template v-for="(it, i) in records">
				<view class="item" :key="'slider_item_'+i" @tap="switchTabTo(it)"
					:style="{background: it.bg, marginRight: i === records.length - 1 ? '15px' : '0px'}">
					<view class="item_content">
						<view class="title">
							<text class="first">{{it.title}}</text>
							<text class="main">主讲：{{it.mainTeacher}}</text>
							<!-- <text class="sub" :style="{color:it.subColor}">2020-09-23</text> -->
						</view>
						<image class="image" :src="it.icon"></image>
						<text class="free">免\n费</text>
					</view>
				</view>
			</template>
		</scroll-view>
	</view>

</template>

<script>
	import commonData  from "@/common/commomData.js"
	export default {
		data() {
			return {
				menus: commonData.menus,
				second_menus:commonData.second_menus,
				records: [{
						bg: 'linear-gradient(-30deg,rgba(171,218,255,1),rgba(215,239,255,1))',
						title: '甲骨文字检测数据集',
						mainTeacher: '殷契文渊',
						subTitle: '认识甲骨文的特点',
						subColor: '#15639F',
						icon: '/static/test2.png',
						url:'/pages/course/course',
						isFree: true
					},
					{
						bg: 'linear-gradient(-30deg,rgba(192,253,227,1),rgba(224,252,240,1))',
						title: '学习甲骨文的方法',
						mainTeacher: '小B',
						subTitle: '了解甲骨文的历史背景和书写方式',
						subColor: '#07B77B',
						icon: '/static/test.png',
						url:'/pages/classification/classification',
						isFree: false
					}
				]
			}
		},
		onLoad() {


		},
		methods: {
			navigateTo(data) {
				uni.navigateTo({
					url: '/pages/details/details?data=' + encodeURIComponent(JSON.stringify(data))
				})
			},
		switchTabTo(item){
				uni.switchTab({
					url: item.url
				});
			}
	
		}
	}

</script>

用到知识点

### uni.navigateTo(OBJECT)

保留当前页面，跳转到应用内的某个页面，使用`uni.navigateBack`可以返回到原页面。

**OBJECT参数说明**

| 参数              | 类型     | 必填 | 默认值 | 说明                                                         | 平台差异说明 |
| :---------------- | :------- | :--- | :----- | :----------------------------------------------------------- | :----------- |
| url               | String   | 是   |        | 需要跳转的应用内非 tabBar 的页面的路径 , 路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，path为下一个页面的路径，下一个页面的onLoad函数可得到传递的参数 |              |
| animationType     | String   | 否   | pop-in | 窗口显示的动画效果，详见：[窗口动画](https://uniapp.dcloud.net.cn/api/router#animation) | App          |
| animationDuration | Number   | 否   | 300    | 窗口动画持续时间，单位为 ms                                  | App          |
| events            | Object   | 否   |        | 页面间通信接口，用于监听被打开页面发送到当前页面的数据。2.8.9+ 开始支持。 |              |
| success           | Function | 否   |        | 接口调用成功的回调函数                                       |              |
| fail              | Function | 否   |        | 接口调用失败的回调函数                                       |              |
| complete          | Function | 否   |        | 接口调用结束的回调函数（调用成功、失败都会执行）             |              |

**object.success 回调函数**

**参数**

**Object res**

| 属性         | 类型                                                         | 说明                 |
| :----------- | :----------------------------------------------------------- | :------------------- |
| eventChannel | [EventChannel](https://uniapp.dcloud.net.cn/api/router#event-channel) | 和被打开页面进行通信 |

**示例**

```
//在起始页面跳转到test.vue页面并传递参数
uni.navigateTo({
	url: 'test?id=1&name=uniapp'
});
```

```
// 在test.vue页面接受参数
export default {
	onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
		console.log(option.id); //打印出上个页面传递的参数。
		console.log(option.name); //打印出上个页面传递的参数。
	}
}


```

### uni.switchTab(OBJECT)

跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面。

**注意：** 如果调用了 [uni.preloadPage(OBJECT)](https://uniapp.dcloud.net.cn/api/preload-page) 不会关闭，仅触发生命周期 `onHide`

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的 tabBar 页面的路径（需在 pages.json 的 tabBar 字段定义的页面），路径后不能带参数 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

**示例**

pages.json

```
{
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index",
      "text": "首页"
    },{
      "pagePath": "pages/other/other",
      "text": "其他"
    }]
  }
}

```

```
uni.switchTab({
	url: '/pages/index/index'
});

```

## xu-sign.vue

```
<canvas 
		    id="canvas"
			canvas-id="canvas"
			@touchmove="move" 
		    @touchstart="start"  
		    @error="error"
			style="border: 1px dotted seagreen"
			@touchend="touchend"
		    :style="{width:canvasWidth + 'px',height:canvasHeight + 'px'}">
		</canvas>
```

[canvas | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/component/canvas.html#canvas)

```
画布。

属性说明

属性名  	类型	 默认值 	说明	 平台差异说明
type	String		指定 canvas 类型，支持 2d (2.9.0) 和 webgl	微信小程序 2.7.0+ 字节小程序1.78.0+
canvas-id	String		canvas 组件的唯一标识符	
disable-scroll	Boolean	false	当在 canvas 中移动时且有绑定手势事件时，禁止屏幕滚动以及下拉刷新	字节跳动小程序与飞书小程序不支持
hidpi	Boolean	true	是否启用高清处理	H5 (HBuilder X 3.4.0+)、App-vue (HBuilder X 3.4.0+)
@touchstart	EventHandle		手指触摸动作开始	字节小程序1.78.0+
@touchmove	EventHandle		手指触摸后移动	字节小程序1.78.0+
@touchend	EventHandle		手指触摸动作结束	字节小程序1.78.0+
@touchcancel	EventHandle		手指触摸动作被打断，如来电提醒，弹窗	字节小程序1.78.0+
@longtap	EventHandle		手指长按 500ms 之后触发，触发了长按事件后进行移动不会触发屏幕的滚动	字节跳动小程序与飞书小程序不支持
@error	EventHandle		当发生错误时触发 error 事件，detail = {errMsg: 'something wrong'}	字节跳动小程序与飞书小程序不支持
```

**注意事项：**

- canvas 标签默认宽度 300px、高度 225px，动态修改 canvas 大小后需要重新绘制。
- h5、app-vue 中单个尺寸过大的 canvas 在 iOS/Safari 无法绘制（具体限制尺寸未公布）。
- 同一页面中的 canvas-id 不可重复，如果使用一个已经出现过的 canvas-id，该 canvas 标签对应的画布将被隐藏并不再正常工作。
- canvas 在微信小程序、百度小程序、QQ小程序中为原生组件，层级高于前端组件，请勿内嵌在 scroll-view、swiper、picker-view、movable-view 中使用。解决 canvas 层级过高无法覆盖，参考 [native-component](https://uniapp.dcloud.net.cn/component/native-component)。其他小程序端的 canvas 仍然为 webview 中的 canvas。
- app-vue 中的 canvas 仍然是 webview 的 canvas。app-nvue下如需使用canvas，需下载插件，详见文档底部章节。
- app-vue的canvas虽然是webview自带的canvas，但却比nvue和微信小程序的原生canvas性能更高。注意并非原生=更快。canvas动画的流畅，关键不在于渲染引擎的速度，而在于减少从逻辑层向视图层频繁通信造成的折损。
- 小程序、app-nvue，因为通信阻塞，难以绘制非常流畅的canvas动画。h5和app-vue不存在此问题。但注意，app-vue下若想流畅的绘制canvas动画，需要使用[renderjs](https://uniapp.dcloud.io/tutorial/renderjs?id=renderjs)技术，把操作canvas的js逻辑放到视图层运行，避免逻辑层和视图层频繁通信。hello uni-app的canvas示例很典型，在相同手机运行该示例，可以看出在h5端和app端非常流畅，而小程序端由于没有renderjs技术，做不到这么流畅的动画。
- **示例：** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/canvas/canvas)

[canvas (dcloud.net.cn)](https://hellouniapp.dcloud.net.cn/pages/component/canvas/canvas)

## `**App.vue**`

#### 是uni-app的主组件，所有页面都是在`App.vue`下进行切换的，是页面入口文件。但`App.vue`本身不是页面，这里不能编写视图元素，也就是没有`<template>`。

这个文件的作用包括：调用应用生命周期函数、配置全局样式、配置全局的存储globalData

应用生命周期仅可在`App.vue`中监听，在页面监听无效。

## [#](https://uniapp.dcloud.net.cn/collocation/App.html#applifecycle)应用生命周期

[uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/collocation/App.html)

```
<style>
	/*每个页面公共css */
	@font-face {
		font-family: "onychia";
		src: url("./static/fonts/onychia.woff");
	}
	@font-face {
		font-family: "AYJGW";
		src: url("./static/fonts/AYJGW.ttf");
	}
	@font-face {
		font-family: "onychia1";
		src: url("./static/fonts/onychia1.woff");
	}
	
	@font-face {
		font-family: "onychia2";
		src: url("./static/fonts/onychia2.woff");
	}
	@font-face {
		font-family: "onychia3";
		src: url("./static/fonts/onychia3.woff");
	}
	@font-face {
		font-family: "onychia4";
		src: url("./static/fonts/onychia4.woff");
	}
	@font-face {
		font-family: "onychia5";
		src: url("./static/fonts/onychia5.woff");
	}
	@font-face {
		font-family: "onychia6";
		src: url("./static/fonts/onychia6.woff");
	}
	@font-face {
		font-family: "onychia7";
		src: url("./static/fonts/onychia7.woff");
	}
	@font-face {
		font-family: "lishu-2";
		src: url("./static/fonts/lishu-2.ttf");
	}
	@font-face {
		font-family: "SanJiKaiShu-2";
		src: url("./static/fonts/SanJiKaiShu-2.ttf");
	}
	
	@font-face {
		font-family: "FZJiaGW-2";
		src: url("./static/fonts/FZJiaGW-2.ttf");
	}
</style>
```

```
style="font-size: 50rpx;font-family: onychia, onychia1, onychia2, onychia3,onychia4,onychia5,onychia6,onychia7,FZJiaGW-2,AYJGW,'Courier New', Courier, monospace;"
```

