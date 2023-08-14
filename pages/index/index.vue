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
					<text class="title">甲骨文书法练习</text>
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
	export default {
		data() {
			return {
				menus: [{
						bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
						icon: '/static/images/js.jpg',
						txt: '祭祀',
						isFree: true,
						//燎、禘、岁、舞、求、卯、戠、取、伐、告、报、沉
						menus_type: [{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '燎',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '禘',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '岁',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '舞',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '求',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '卯',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '戠',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '取',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '伐',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '告',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '报',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '沉',
								isFree: true
							},
						],
					},
					{
						bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
						icon: '/static/images/tianqi.jpg',
						txt: '气候',
						isFree: false,
						//气、象、风、云、雨、雪、雷、雾、霾、虹、水、火、日、月
						menus_type: [{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '气',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '象',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '风',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '云',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '雨',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '雪',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '雷',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '雾',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '霾',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '虹',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '水',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '火',
								isFree: true
							},
						],
					},
					{
						bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
						icon: '/static/images/zfa.png',
						txt: '征伐',
						isFree: true,
						//武、帛、刀、鼓、车、马、兵、死、伤、征、伐、侵
						menus_type: [{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '武',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '帛',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '刀',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '鼓',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '车',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '马',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '兵',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '伤',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '伐',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '征',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '侵',
								isFree: false
							},
						],
					},

				],
				second_menus: [
					{
						icon: '/static/images/tianlie.png',
						txt: '田猎',
						//犬、牛、羊、弓、狗、牛、矛、旄（mao）、熊、鹿
						menus_type: [{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '犬',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '牛',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '羊',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '弓',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '狗',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '牛',
								isFree: false
							},
							// {
							// 	bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
							// 	icon: '/static/emblem.png',
							// 	txt: '矛',
							// 	isFree: true
							// },
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '矛',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '熊',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '鹿',
								isFree: false
							}
						],
					},
					// {
					// 	icon: '/static/textbook.png',
					// 	/**病（bìng）- 表示疾病
					// 	疹（zhěn）- 表示皮肤上的疹子
					// 	疳（gān）- 表示慢性营养不良症状
					// 	瘀（yū）- 表示淤血或瘀伤
					// 	瘤（liú）- 表示肉体上的瘤，如瘤子
					// 	痔（zhì）- 表示痔疮
					// 	痹（bì）- 表示关节或肌肉僵硬**/

					// 	txt: '病患',
					// 	menus_type: [{
					// 			bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
					// 			icon: '/static/graduation.png',
					// 			txt: '病',
					// 			isFree: true
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
					// 			icon: '/static/live.png',
					// 			txt: '疹',
					// 			isFree: false
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
					// 			icon: '/static/emblem.png',
					// 			txt: '痛',
					// 			isFree: true
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
					// 			icon: '/static/question_bank.png',
					// 			txt: '伤',
					// 			isFree: true
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
					// 			icon: '/static/graduation.png',
					// 			txt: '瘤',
					// 			isFree: true
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
					// 			icon: '/static/live.png',
					// 			txt: '死',
					// 			isFree: false
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
					// 			icon: '/static/question_bank.png',
					// 			txt: '痹',
					// 			isFree: true
					// 		},
					// 		{
					// 			bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
					// 			icon: '/static/question_bank.png',
					// 			txt: '老',
					// 			isFree: true
					// 		},
					// 	],
					// },
					{
						icon: '/static/images/sy.jpg',
						/**子（zǐ）- 表示儿子，也可以表示后代
						卵（luǎn）- 表示鸟类的卵，也可以指人类的卵子
						男（nán）- 表示男性
						女（nǚ）- 表示女性
						仝（tóng）- 表示同胞兄弟姐妹
						婴（yīng）- 表示新生儿
						腹（fù）- 表示肚子，也可以指怀孕
						孕（yùn）- 表示怀孕**/
						txt: '生育',
						menus_type: [{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '子',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '卵',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '男',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '女',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '婴',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '腹',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '孕',
								isFree: true
							},
							// {
							// 	bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
							// 	icon: '/static/question_bank.png',
							// 	txt: '腹',
							// 	isFree: true
							// },
						],
					},
					{
						icon: '/static/images/chumen.jpeg',
						/** 出（chū）- 表示出门
						入（rù）- 表示进门
						门（mén）- 表示门
						道（dào）- 表示路
						往（wǎng）- 表示往某个地方去
						坻（dǐ）- 表示陆地
						水（shuǐ）- 表示水路
						舟（zhōu）- 表示船只**/
						txt: '出门',
						menus_type: [{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '出',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(251,184,35,1),rgba(255,228,40,1))',
								icon: '/static/live.png',
								txt: '入',
								isFree: false
							},
							{
								bg: 'linear-gradient(0deg,rgba(255,126,34,1),rgba(240,184,27,1))',
								icon: '/static/emblem.png',
								txt: '门',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '道',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,216,162,1),rgba(90,242,217,1))',
								icon: '/static/graduation.png',
								txt: '往',
								isFree: true
							},
							{
								bg: 'linear-gradient(0deg,rgba(9,177,252,1),rgba(24,200,255,1))',
								icon: '/static/question_bank.png',
								txt: '舟',
								isFree: true
							},
						],
						
					}
				],

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
					// {
					// 	bg: 'linear-gradient(-30deg,rgba(171,218,255,1),rgba(215,239,255,1))',
					// 	title: '教师考情分析',
					// 	mainTeacher: '小A',
					// 	subTitle: '标题名称',
					// 	subColor: '#15639F',
					// 	icon: '/static/test2.png',
					// 	isFree: true
					// }
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

<style>
	page {
		width: 100%;
		background-color: #ebebeb;
	}
</style>
<style lang="scss" scoped>
	@function realSize($args) {
		@return $args / 1.5;
	}

	.page_edu {
		width: 100%;
	}

	.page_edu_header {
		padding-top: var(--status-bar-height);
		background-color: #0bc99d;
		width: 100%;
		height: realSize(415px);

		.header {
			display: flex;
			flex-direction: row;
			align-items: center;
			padding: realSize(20px);

			.btn {
				width: realSize(36px);
				height: realSize(30px);
			}

			.input {
				height: realSize(59px);
				width: 100%;
				margin-left: realSize(20px);
				margin-right: realSize(20px);
				background: rgba(255, 255, 255, 1);
				border-radius: realSize(30px);
				display: flex;
				flex-direction: row;
				align-items: center;

				.search {
					width: realSize(30px);
					height: realSize(30px);
					margin-left: realSize(20px);
					margin-right: realSize(20px);
				}
			}
		}

		.header_content {
			display: flex;
			flex-direction: row;

			.left {
				display: flex;
				flex-direction: column;
				width: 57%;
				margin-top: 10px;
				margin-left: 15px;
				margin-right: 15px;

				.title {
					width: realSize(419px);
					height: realSize(59px);
					font-size: realSize(47px);
					font-weight: bold;
					color: rgba(255, 255, 255, 1);
				}

				.sub_title {
					margin-top: 3px;
					font-size: realSize(18px);
					font-weight: 400;
					color: rgba(255, 255, 255, 1);

					background: linear-gradient(0deg, rgba(120, 255, 224, 1) 0%, rgba(255, 255, 255, 1) 100%);
					-webkit-background-clip: text;
					-webkit-text-fill-color: transparent;
				}

				.btn {
					margin-top: 3px;
					width: realSize(198px);
					height: realSize(60px);
					background: linear-gradient(-30deg, rgba(252, 135, 29, 1), rgba(246, 185, 9, 1));
					box-shadow: 0px 4px 10px 0px rgba(255, 121, 0, 0.5);
					border-radius: realSize(30px);
					color: rgba(255, 255, 255, 1);
					display: flex;
					align-items: center;
					justify-content: center;
				}
			}
		}
	}

	.page_content {
		width: 100%;
		margin-top: 10px;

		.menu {
			margin-left: 10px;
			margin-right: 10px;
			padding-left: 40px;
			padding-right: 40px;
			height: realSize(200px);
			background: rgba(255, 255, 255, 1);
			box-shadow: 0px 10px 10px 0px rgba(0, 161, 124, 0.1);
			// border-radius: 10px;
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
					width: realSize(100px);
					height: realSize(100px);
					border-radius: 30px;
					display: flex;
					align-items: center;
					background-size: cover;
					// border-radius: 30px;
					justify-content: center;

					.image {
						width: 100%;
						height: 100%;
						border-radius: 30px;
					}
				}

				.txt {
					margin-top: 5px;
					font-size: 14px;
					color: rgba(51, 51, 51, 1);
				}
			}
		}

		.s_menu {
			display: flex;
			flex-direction: row;
			align-items: stretch;
			justify-content: space-between;
			margin-top: 15px;
			margin-left: 10px;
			margin-right: 10px;
			padding-left: 10px;
			padding-right: 10px;

			.item {
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;

				.image {
					width: 35px;
					height: 35px;
				}

				.txt {
					margin-top: 5px;
					font-size: 14px;
					color: rgba(51, 51, 51, 1);
				}
			}
		}

		.ad {
			width: 100%;
			display: flex;
			flex-direction: row;
			align-items: center;
			justify-content: center;

			.bg {
				position: absolute;
				width: 120px;
				height: 105px;
				left: 0;
			}

			.ad_btn {
				width: 100%;
				height: 63px;
				margin: 30px;
				background: linear-gradient(0deg, rgba(253, 155, 28, 1), rgba(251, 197, 33, 1));
				border-radius: 67px;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;

				.title {
					font-size: realSize(38px);
					font-family: PingFang-SC-Heavy;
					font-weight: 800;
					color: rgba(255, 255, 255, 1);
				}

				.sub_title {
					background: linear-gradient(0deg, rgba(255, 128, 37, 1), rgba(255, 153, 32, 1));
					box-shadow: 0px 4px 5px 0px rgba(92, 53, 48, 0.3), 0px 1px 0px 0px rgba(228, 228, 228, 1);
					border-radius: realSize(24px);
					font-size: realSize(24px);
					font-family: PingFang-SC-Heavy;
					font-weight: 800;
					font-style: italic;
					color: rgba(255, 236, 177, 1);
					line-height: realSize(26px);
				}
			}
		}
	}

	.slider {
		white-space: nowrap;
		width: 100%;
		background-color: white;

		.item {
			display: inline-block;
			margin-left: 15px;
			margin-top: 13px;
			margin-bottom: 13px;
			width: 60%;
			height: 125px;
			border-radius: 10px;

			.item_content {
				display: flex;
				flex-direction: row;

				.title {
					width: 36%;
					margin: 20px;
					display: flex;
					flex-direction: column;

					.first {
						font-size: 16px;
						color: rgba(46, 65, 69, 1);
					}

					.main {
						font-size: 13px;
						color: rgba(79, 103, 101, 1);
						margin-top: 5px;
					}

					.sub {
						width: 60px;
						font-size: 10px;
						margin-top: 20px;
						background: rgba(255, 255, 255, 0.4);
						border-radius: 5px;
						display: flex;
						align-items: center;
						justify-content: center;
					}
				}

				.image {
					margin-top: 35px;
					width: 80px;
					height: 80px;
				}

				.free {
					background: rgba(11, 147, 252, 1);
					border-radius: 0px 0px 22px 22px;
					width: 25px;
					height: 50px;
					display: flex;
					align-items: center;
					justify-content: center;
					color: #FFFFFF;
					font-size: 14px;
				}
			}
		}
	}
</style>