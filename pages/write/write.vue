<template>
	<view class="">
		<view class="uni-padding-wrap uni-common-mt" style="height: 30%; display: flex;justify-content: center;" >
			<text
				style="font-size: 30vh;font-family: onychia, onychia1, onychia2, onychia3,onychia4,onychia5,onychia6,onychia7,FZJiaGW-2,'Courier New', Courier, monospace;">{{writeFont.txt}}</text>
			<!-- canvas -->
			<!-- <canvas class="mycanvas" canvas-id="mycanvas" @touchstart="touchstart" @touchmove="touchmove" @touchend="touchend"></canvas> -->

			<!-- 底部操作按钮 -->
			<!-- 	<view class="uni-flex uni-row">
			<view class="flex-item uni-badge-yellow" @click='createCanvas()'>点击触发写字板</view>
		</view>
		<view class="uni-flex uni-row">
			<view class="flex-item uni-bg-red" @click="finish">保存</view>
			<view class="flex-item uni-bg-green" @click="clear">清除</view>
			<view class="flex-item uni-bg-blue"  @click="clear">关闭</view>
		</view> -->
		</view>
		<view class="" style=""> 
			<xu-sign @finish="finish" :height="500"></xu-sign>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(e) {
			console.log(e.data, "22222222222");
			if (e && e.data !== 'underfind') {
				this.writeFont = JSON.parse(e.data);
			}

		},
		data() {
			return {
				//临摹汉字
				writeFont: '',
				title:'甲骨文临摹',
				//绘图图像
				ctx: '',
				//路径点集合
				points: [],
				//签名图片
				SignatureImg: ''
			}
		},
		methods: {
			createCanvas() {
				//创建绘图对象
				this.ctx = uni.createCanvasContext('mycanvas', this);
				//设置画笔样式
				this.ctx.lineWidth = 4;
				this.ctx.lineCap = 'round';
				this.ctx.lineJoin = 'round';
			},
			touchstart(e) {
				let startX = e.changedTouches[0].x;
				let startY = e.changedTouches[0].y;
				let startPoint = {
					X: startX,
					Y: startY
				};
				this.points.push(startPoint);
				//每次触摸开始，开启新的路径
				this.ctx.beginPath();
			},
			touchmove(e) {
				let moveX = e.changedTouches[0].x;
				let moveY = e.changedTouches[0].y;
				let movePoint = {
					X: moveX,
					Y: moveY
				};
				this.points.push(movePoint); //存点
				let len = this.points.length;
				if (len >= 2) {
					this.draw(); //绘制路径
				}
			},
			touchend() {
				this.points = [];
			},
			draw() {
				let point1 = this.points[0];
				let point2 = this.points[1];
				this.points.shift();
				this.ctx.moveTo(point1.X, point1.Y);
				this.ctx.lineTo(point2.X, point2.Y);
				this.ctx.stroke();
				this.ctx.draw(true);
			},
			clear() {
				let that = this;
				uni.getSystemInfo({
					success: function(res) {
						console.log(res,"res");
						let canvasw = res.windowWidth;
						let canvash = res.windowHeight;
						that.ctx.clearRect(0, 0, canvasw, canvash);
						that.ctx.draw(true);
					}
				});
			},
			finish(res) {
				console.log(this.writeFont.txt, "1111")
				
				uni.navigateTo({
					url: '/pages/explain/explain?data=' + encodeURIComponent(JSON.stringify(this.writeFont.txt))
				})
				// let that = this;
				// uni.canvasToTempFilePath({
				//     canvasId: 'mycanvas',
				//     success: function(res) {
				//              //这里的res.tempFilePath就是生成的签字图片
				//             console.log(res.tempFilePath);
				//     }
				// });
			}
		}

	}
</script>

<style scoped>
	page {
		width: 100%;
		height: 100%;
	}
	/* .mycanvas {
		width: 300px;
		height: 500px;
	}

	.flex-item {
		width: 33.3%;
		height: 200rpx;
		text-align: center;
		line-height: 200rpx;
	}

	.flex-item-V {
		width: 100%;
		height: 150rpx;
		text-align: center;
		line-height: 150rpx;
	}

	.text {
		margin: 15rpx 10rpx;
		padding: 0 20rpx;
		background-color: #ebebeb;
		height: 70rpx;
		line-height: 70rpx;
		text-align: center;
		color: #777;
		font-size: 26rpx;
	}

	.flex-pc {
		display: flex;
		justify-content: center;
	} */
</style>