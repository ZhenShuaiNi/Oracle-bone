<template>
	<view class="container">
		<view class="left">
			<view @click="choice(index)" :class="{'active':index==current}" v-for="(item,index) in classify" :key="index">{{item}}</view>
		</view>
		<view class="right">
			<view class="title">
				<view>甲骨文学习</view>
				<view>学习甲骨文入门首选</view>
			</view>
			<view class="content">
				<view class="detail" v-for="(item,index) in name" :key="index">
					<image src="../../static/images/js.jpg"></image>
					<view style="font-size: 50rpx;font-family: onychia, onychia1, onychia2, onychia3,onychia4,onychia5,onychia6,onychia7,FZJiaGW-2,AYJGW">{{item}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				classify:["祭祀","气候","征伐","田猎","生育","出门"],
				name:["燎","禘","岁","舞","求","卯","戠","取","伐","告","报","沉"],
				image_url:["../../static/js.jpg"],
				index:0,
				current:0
			}
		},
		methods:{
			choice(index){
				this.index=index,
				this.current=index
			}
		}
	}
</script>

<style scoped>
	.container{
		display: flex;
		height: 100vh;
	}
	.left{
		width: 220rpx;
		background-color: #e4e3e3;
		color: #616161;
		padding:40rpx 15rpx 40rpx 20rpx;
		border-radius: 0rpx 20rpx 20rpx 0rpx;
		margin-right: 20rpx;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		font-size: 30rpx;
		font-weight: 700;
		align-items: stretch;
	}
	.left view{
		display: flex;
		align-items: center;
		height: 90rpx;
	}
	.active{
		color: #dd1705;
		position: relative;
	}
	.active::before{
		content: "";
		position: absolute;
		width: 8rpx;
		height: 20rpx;
		background-color: #dd1705;
		left: -12rpx;
		top: 39rpx;
		border-radius: 25rpx;
	}
	.right{
		width: 500rpx;
		padding-bottom: 20rpx;
	}
	.right .title{
		width: 500rpx;
		height: 170rpx;
		line-height: 66rpx;
		background-image: linear-gradient(45deg,rgb(223, 87, 8),rgb(245, 153, 67));
		border-radius: 15rpx;
		box-sizing: border-box;
		padding-top: 20rpx;
		box-shadow: 0rpx 5rpx 5rpx 0rpx #CCCCCC;
	}
	.title view{
		text-align: center;
		color: white;
		font-size: 29rpx;
	}
	.title view:nth-of-type(1){
		font-size: 40rpx;
		font-weight: 600;
	}
	.content{
		display: flex;
		flex-wrap: wrap;
		align-content: flex-start;
	}
	.detail{
		display: flex;
		flex-direction: column;
		text-align: center;
		width: 150rpx;
		height: 150rpx;
		margin:30rpx 10rpx 0rpx 0rpx ;
		font-size: 27rpx;
		color: #646464;
	}
	.detail image{
		width: 90rpx;
		height: 90rpx;
		border-radius: 50%;
		margin: auto;
	}
</style>