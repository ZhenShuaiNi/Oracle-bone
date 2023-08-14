<template>
	<view class="xu-sign ">
		<template v-if="orientation == 'abeam'">
			<view class="sighButtons" >
				<view class="sighButtons_button" style="border: solid 1rpx #999; color: #999;background-color: #fff;margin-top: 100rpx;"  @click.tap="back">
					<p class="sighButtons_button_xiao">返回</p>
				</view>
				<view class="sighButtons_button" style="background: #999;" @click.tap="clearClick">
					<view class="sighButtons_button_xiao">重签</view>
				</view>
				<view class="sighButtons_button" style="background-color: #38A99A;" @click.tap="finish">
					<view class="sighButtons_button_xiao">完成签名</view>
				</view>
			</view>
		</template>
		<canvas 
		    id="canvas"
			canvas-id="canvas"
			@touchmove="move" 
		    @touchstart="start"  
		    @error="error"
			@touchend="touchend"
		    :style="{width:canvasWidth + 'px',height:canvasHeight + 'px'}">
		</canvas>
		<template v-if="orientation == 'portrait'">
			<view class="sighButton " >
				<view class="sighButton_button" style="border: solid 1rpx #999; color: #999;background-color: #fff;" @click.tap="createCanvas">
					<p class="sighButton_button_xiao">开始临摹</p>
				</view>
				<view class="sighButton_button" style="background: #999;" @click.tap="clearClick">
					<view class="sighButton_button_xiao">清除</view>
				</view>
				<view class="sighButton_button" style="background-color: #38A99A;" @click.tap="finish">
					<view class="sighButton_button_xiao">完成临摹</view>
				</view>
				<view class="sighButton_button" style="border: solid 1rpx #999; color: #999;background-color: #fff;" @click.tap="back">
					<p class="sighButton_button_xiao">返回</p>
				</view>
			</view>
		</template>
	</view>
</template>

<script>
	export default {
		name:"xu-sign",
		props:{
			orientation:{
				type: String,
				default: 'portrait'
			},
			width:{
				type: Number,
				default: 0
			},
			height:{
				type: Number,
				default: 0
			},
			lineWidth:{
				type:Number,
				default:3
			},
			strokeStyle:{
				type:String,
				default:"black"
			}
		},
		data() {
			return {
				canvas: '',
				ctx: '',
				pr:0,
				canvasWidth:'',
				canvasHeight:'',
				points:[]
			};
		},
		created(){
			this.getSystemInfo();
			// this.createCanvas();
		},
		methods:{
			// 触摸开始
			start(e) {
				this.points.push({X:e.touches[0].x,Y:e.touches[0].y});
				//每次触摸开始，开启新的路径
				this.ctx.beginPath();
			},
			// 开始移动
			move(e) {
				this.points.push({X:e.touches[0].x,Y:e.touches[0].y});       //存点
				if(this.points.length >= 2){
					this.draw();                   //绘制路径
				}
			},
			// 触摸结束，将未绘制的点清空防止对后续路径产生干扰
			touchend(){                  
				this.points=[];
			},
			/* ***********************************************
			   绘制笔迹
			   1.为保证笔迹实时显示，必须在移动的同时绘制笔迹
			   2.为保证笔迹连续，每次从路径集合中区两个点作为起点（moveTo）和终点(lineTo)
			   3.将上一次的终点作为下一次绘制的起点（即清除第一个点）
			************************************************ */
			draw(){
				let point1 = this.points[0];
				let point2 = this.points[1];
				this.points.shift();
				this.ctx.moveTo(point1.X, point1.Y);
				this.ctx.lineTo(point2.X, point2.Y);
				this.ctx.stroke();
				this.ctx.draw(true);
			},
			error(e) {
				console.log("画布触摸错误" + e);
			},
			// 点击完成签名
			finish(){
				uni.canvasToTempFilePath({
					canvasId: 'canvas',
					success: (res) => {
						let path = res.tempFilePath;
						this.$emit("finish",path);
						// console.log(res.tempFilePath)
					}
				})
			},
			//重签
			clearClick () {
			    //清除画布
			    this.ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
				this.ctx.draw(true);
			},
			// 返回事件
			back(){
				uni.navigateBack();
			},
			createCanvas() {
				const pr = this.pr; // 像素比
				const ctx = uni.createCanvasContext('canvas',this);
				ctx.lineGap = 'round';
				ctx.lineJoin = 'round';
				ctx.lineWidth = this.lineWidth; // 字体粗细
				ctx.strokeStyle = this.strokeStyle; // 字体粗细
				this.ctx = ctx;
			},
			 // 获取系统信息
			getSystemInfo() {
				uni.getSystemInfo({
					success:(res) => {
						console.log(res,"res_______");
						this.pr = res.pixelRatio;
						if(this.orientation == 'portrait'){
							if(this.width > res.windowWidth || this.width == 0){
								this.canvasWidth = res.windowWidth;
							}else {
								this.canvasWidth = this.width;
							}
							if(this.height > res.windowHeight - 100  || this.height == 0){
								this.canvasHeight = res.windowHeight - 100;
							}else{
								this.canvasHeight = this.height;
							}
						}else if(this.orientation == 'abeam'){
							if(this.width > res.windowWidth - 100 || this.width == 0){
								this.canvasWidth = res.windowWidth - 100;
							}else {
								this.canvasWidth = this.width;
							}
							if(this.height > res.windowHeight  || this.height == 0){
								this.canvasHeight = res.windowHeight ;
							}else{
								this.canvasHeight = this.height;
							}
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	page {
		width: 100%;
		height: 100%;
	    background-color: #e9f2f1;
	}
	canvas {
		background-color: white;
	}
	.xu-sign{
		width: 100%;
		height: 100%;
		display: flex;
		flex-wrap: wrap;
		align-items: flex-end;
	}
	.sighButton{
		width: 690rpx;
		margin: 0rpx auto;
		height: 60px;
		padding-top:10px;
		display: flex;
		justify-content: space-between;
		&_button{
			width: 20%;
			height: 100rpx;
			border-radius: 10rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			font-size: 32rpx;
			color: #fff;
		}
		
	}
	.sighButtons{
		width:70px;
		margin: 0rpx auto;
		height: 600rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		&_button{
			width: 200rpx;
			height: 55px;
			border-radius: 10rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			font-size: 32rpx;
			color: #fff;
			transform: rotate(90deg);
		}
		
	}
</style>