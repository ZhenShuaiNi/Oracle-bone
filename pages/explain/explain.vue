<template>
	<view>
		<view class="">
			<page-head style="height:100rpx;display: flex;justify-content: center;font-size: 50rpx;color: #e15707c7;
			align-items: center;" :title="title"></page-head>
			<view class="menu">
				<view class="item">
					<view
						style="font-size: 100rpx;font-family: onychia, onychia1, onychia2, onychia3,onychia4,onychia5,onychia6,onychia7,FZJiaGW-2,AYJGW,'Courier New', Courier, monospace;">
						{{fontWrite}}
					</view>
				</view>
				<uni-icons type="arrow-right" size="50" class="iconP"></uni-icons>
				<view style="font-size: 100rpx;font-family:lishu-2, Courier, monospace;" class="">
					{{fontWrite}}
				</view>
				<uni-icons type="arrow-right" size="50" class="iconP"></uni-icons>
				<view class="" style=" font-size: 100rpx;font-family:SanJiKaiShu-2, Courier, monospace;">
					{{fontWrite}}
				</view>
			</view>
		</view>
		<view class="menu" style="height: 50%;margin-top:10vh;">
			<text class="txt" style="font-size: 50rpx;font-family:lishu-2, Courier, monospace;">解释:</text>
			<text class="txt">
				病（bìng）- 表示疾病
				疹（zhěn）- 表示皮肤上的疹子
				疳（gān）- 表示慢性营养不良症状
				瘀（yū）- 表示淤血或瘀伤
				瘤（liú）- 表示肉体上的瘤，如瘤子
				痔（zhì）- 表示痔疮
				痹（bì）- 表示关节或肌肉僵硬**
				子（zǐ）- 表示儿子，也可以表示后代
				卵（luǎn）- 表示鸟类的卵，也可以指人类的卵子
				男（nán）- 表示男性
				女（nǚ）- 表示女性
				仝（tóng）- 表示同胞兄弟姐妹
				婴（yīng）- 表示新生儿
				腹（fù）- 表示肚子，也可以指怀孕
				孕（yùn）- 表示怀孕
				出（chū）- 表示出门
				入（rù）- 表示进门
				门（mén）- 表示门
				道（dào）- 表示路
				往（wǎng）- 表示往某个地方去
				坻（dǐ）- 表示陆地
				水（shuǐ）- 表示水路
				舟（zhōu）- 表示船只
			</text>
		</view>
		<view class="flex-item">
		<navigator url="/pages/index/index"><button  type="default"  @tap="switchTabTo">返回</button></navigator>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(e) {
			if (e && e.data !== 'underfind') {
				this.fontWrite = JSON.parse(e.data);
			}
		},
		data() {
			return {
				title: '说文解字',
				fontWrite: ''

			}
		},
		methods: {
			switchTabTo(){
				uni.switchTab({
					url:"/pages/index/index"
				});
				
			}

		}
	}
</script>

<style scoped>
	page {
		width: 100%;
		height: 100%;
	}

	.iconP {
		position: relative;
		top: 40rpx;
	}

	.menu {
		margin-top: 50rpx;
		margin-left: 20px;
		margin-right: 20px;
		padding-left: 10px;
		padding-right: 10px;
		height: realSize(176px);
		background: rgba(255, 255, 255, 1);
		box-shadow: 0px 10px 10px 0px rgba(0, 161, 124, 0.1);
		border-radius: 10px;
		display: flex;
		flex-direction: row;
		align-items: stretch;
		justify-content: space-between;

		.item {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;

			.img_view {
				width: 60px;
				height: 60px;
				border-radius: 30px;
				display: flex;
				align-items: center;
				justify-content: center;

				.image {
					width: 50px;
					height: 50px;
				}
			}

			.txt {
				margin-top: 5px;
				font-size: 14px;
				color: rgba(51, 51, 51, 1);
			}
		}
		.flex-item {
			width: 33.3%;
			height: 200rpx;
			text-align: center;
			line-height: 200rpx;
		}

	}
</style>