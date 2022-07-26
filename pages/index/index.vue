<template>
	<scroll-view
		:scroll-top="scrollTop"
		scroll-y="true" 
		class="content" 
		@scroll="scroll">
		<!-- 顶部 -->
		<view :class="fixedTop?'top-cont fixed':'top-cont'">
			<!-- 状态栏 -->
			<view class="status-bar" :style="{height: statusBarHeight +'px'}"></view>
			<!-- 定位 -->
			<view class="location-box">
				<image class="locat white" src="../../static/images/icon_locat.png" mode=""></image>
				<image class="locat black" src="../../static/images/icon_locat_b.png" mode=""></image>
				<text class="locat-text">盐锅峡电厂住宅区</text>
				<image class="arrow" src="../../static/images/icon_arrow_d.png" mode=""></image>
			</view>
			<!-- 搜索栏 -->
			<view class="search-box" @click="showSearch">
				<image class="img" src="../../static/images/icon_search.png" mode=""></image>
				<input type="text" placeholder="搜索附近的商家、商品" placeholder-class="input-place">
			</view>
			<!-- 分类 -->
			<scroll-view scroll-x="true" class="top-cate-box">
				<view class="inner">
					<view v-for="(item,index) in 16" :key="index" class="item">
						金河{{ index }}
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="content-inner">
			
			<!-- 菜单 -->
			<view class="menu-cont">
				<func-menu :list="menuList" />
			</view>
			<!-- 签到等 -->
			<view class="small-menu-box">
				<view class="item">
					<image class="img" src="../../static/images/icon_signin.png" mode=""></image>
					<text class="text">签到</text>
				</view>
				<view class="line"></view>
				<view class="item">
					<image class="img" src="../../static/images/icon_signin.png" mode=""></image>
					<text class="text">领券中心</text>
				</view>
				<view class="line"></view>
				<view class="item">
					<image class="img" src="../../static/images/icon_signin.png" mode=""></image>
					<text class="text">免费水果</text>
				</view>
				<view class="line"></view>
				<view class="item">
					<image class="img" src="../../static/images/icon_signin.png" mode=""></image>
					<text class="text">领现金</text>
				</view>
			</view>
			<!-- 附近商家 -->
			<view class="nearby-merchants">
				<view class="title-box">
					<text class="label">附近商家</text>
					<view class="show-more" @click="showMoreBusi">
						<text class="text">查看更多</text>
						<image class="img" src="../../static/images/icon_arrow_r.png" mode=""></image>
					</view>
				</view>
				<!-- 商家分类 -->
				<scroll-view scroll-x="true">
					<view class="busi-cate"> 
						<view v-for="(item,index) in 10" :key="index" :class="activeBusiCate == index?'item active':'item'">
							全部
						</view>
					</view>
				</scroll-view>
				<!-- 商家列表 -->
				<scroll-view scroll-x="true">
					<view class="busi-list">
						<view v-for="(item,index) in 10" :key="index" class="item" @click="showBusiDet">
							<view class="adver-box">
								<image class="adver" src="../../static/logo.png" mode="aspectFill"></image>
								<image class="logo" src="../../static/logo.png" mode="aspectFill"></image>
							</view>
							<view class="info-box">
								<view class="name ellipsis">北京华联很差很差很差</view>
								<!-- 劵 -->
								<view v-if="index == 0" class="securit">领12元叠加券</view>
								<!-- 预定时间 -->
								<view v-else class="time ellipsis">接受预定 明日09:00</view>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
			<!-- 商品分类 -->
			<scroll-view class="goods-cate-scroll" scroll-x="true">
				<view class="goods-cate">
					<view :class="goodsCateActive ==1?'item active':'item'" @click="goodsCateSelect(1)">
						<text class="label">精选</text>
						<text class="text">优选好物</text>
					</view>
					<view class="line"></view>
					<view :class="goodsCateActive ==2?'item active':'item'" @click="goodsCateSelect(2)">
						<text class="label">打牌热卖</text>
						<text class="text">天天抽奖</text>
					</view>
					<view class="line"></view>
					<view :class="goodsCateActive ==3?'item active':'item'" @click="goodsCateSelect(3)">
						<text class="label">买菜做饭</text>
						<text class="text">菜肉粮油</text>
					</view>
					<view class="line"></view>
					<view :class="goodsCateActive ==4?'item active':'item'" @click="goodsCateSelect(4)">
						<text class="label">水果</text>
						<text class="text">时令新品</text>
					</view>
				</view>
			</scroll-view>
			<!-- 子分类 -->
			<view v-if="goodsCateActive == 3" class="sub-cate">
				<view class="item active">全部</view>
				<view class="item">蔬菜</view>
				<view class="item">蛋</view>
				<view class="item">米面粮油</view>
				<view class="item">面点熟食</view>
				<view class="item">调味品</view>
			</view>
			<!-- 商品列表 -->
			<view class="goods-list">
				<view v-for="(item,index) in 10" :key="index" class="item">
					<view class="img-box">
						<image src="../../static/logo.png" mode="aspectFit"></image>
						<!-- 活动 -->
						<view class="act-title">2件预估单价</view>
						<view class="act-num">￥46.9</view>
					</view>
					<view class="info-box">
						<view class="goods-name ellipsis2">金龙鱼醇香菜籽油(非转压榨)5L</view>
						<!-- 优惠 -->
						<view class="offers">
							<view class="item">满99减12</view>
							<view class="item">满79减8</view>
							<view class="item">满59减6</view>
						</view>
						<!-- 价格 -->
						<view class="price">￥89.9</view>
						<!-- 店铺 -->
						<view class="shop-info">
							<view class="logo">
								<image src="../../static/logo.png" mode="aspectFill"></image>
							</view>
							<view class="inner">
								<view class="name ellipsis">北京华联换卡率深刻的骄傲肯定</view>
								<view class="freight">运费￥4.5</view>
							</view>
						</view>
					</view>
				</view>
				<view v-for="(item,index) in 13" :key="index" class="item">
					<view class="img-box">
						<image src="../../static/logo.png" mode="aspectFit"></image>
						<!-- 活动 -->
						<view class="act-title">2件预估单价</view>
						<view class="act-num">￥46.9</view>
					</view>
					<view class="info-box">
						<view class="goods-name ellipsis2">金龙鱼醇香</view>
						<!-- 优惠 -->
						<view class="offers">
							<view class="item">满99减12</view>
							<view class="item">满79减8</view>
							<view class="item">满59减6</view>
						</view>
						<!-- 价格 -->
						<view class="price">￥89.9</view>
						<!-- 店铺 -->
						<view class="shop-info">
							<view class="logo">
								<image src="../../static/logo.png" mode="aspectFill"></image>
							</view>
							<view class="inner">
								<view class="name ellipsis">北京华联</view>
								<view class="freight">运费￥4.5</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</scroll-view>
</template>

<script>
	import funcMenu from '@/components/menu/index.vue'
	export default {
		components: { funcMenu },
		data() {
			return {
				fixedTop: false, // 是否固定头部搜索框
				statusBarHeight: uni.getStorageSync('statusBarHeight'),
				scrollTop: 0,
				activeBusiCate: 0, // 选中的附近商家分类
				goodsCateActive: 1, // 选中的商品类型
				// 菜单列表
				menuList: [
					{
						uniapp_url: './cateList',
						name: '超市',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '生鲜果蔬',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '乳制品',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '粮油副食',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '送药上门',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '个洗家清',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '母婴',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '酒水饮料',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '家居家装',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '烘焙蛋糕',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					},
					{
						name: '手机家电',
						pic: 'http://t15.baidu.com/it/u=4007473826,3396966131&fm=224&app=112&f=JPEG?w=500&h=500'
					}
				]
			}
		},
		onLoad() {

		},
		methods: {
			scroll(e) {
				if(e.detail.scrollTop >= 10) {
					this.fixedTop = true
				} else {
					this.fixedTop = false
				}
			},
			// 商品类型选择
			goodsCateSelect(index) {
				this.goodsCateActive = index
			},
			// 商家
			showBusiDet() {
				uni.navigateTo({
					url: './business'
				})
			},
			// 搜索
			showSearch() {
				uni.navigateTo({
					url: './search'
				})
			},
			// 附近商家
			showMoreBusi() {
				uni.navigateTo({
					url: './nearbyBusi'
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
</style>

<style scoped lang="scss">
	.content{
		height: 100%;
		position: relative;
		.top-cont{
			background-color: #00cf37;
			padding: 0 20upx;
			transition: all .5s;
			.location-box{
				height: 88upx;
				line-height: 88upx;
				display: flex;
				align-items: center;
				padding-left: 6upx;
				.locat{
					width: 36upx;
					height: 36upx;
					&.black{
						display: none;
						transition: all .5s;
					}
				}
				.locat-text{
					font-size: 28upx;
					color: #fff;
					margin: 0 10upx;
					
				}
				.arrow{
					width: 32upx;
					height: 32upx;
				}
			}
			.search-box{
				height: 60upx;
				line-height: 60upx;
				border-radius: 30upx;
				background-color: #fff;
				padding: 0 30upx;
				display: flex;
				align-items: center;
				transition: all .5s;
				.img{
					width: 30upx;
					height: 30upx;
					margin-right: 10upx;
				}
				input{
					flex: 1;
					font-size: 24upx;
					color: #000;
				}
				.input-place{
					font-size: 24upx;
					color: #878787;
				}
			}
			.top-cate-box{
				padding: 16upx 0;
				.inner{
					display: flex;
					align-items: center;
				}
				.item{
					flex-shrink: 0;
					height: 36upx;
					line-height: 36upx;
					padding: 0 20upx;
					border-radius: 18upx;
					font-size: 26upx;
					color: #fff;
					background-color: #17d34b;
					margin-right: 20upx;
					&:last-child{
						margin-right: 0;
					}
				}
			}
			&.fixed{
				background-color: #fff;
				position: fixed;
				top: 0;
				left: 0;
				z-index: 99;
				width: 100%;
				box-shadow: 0px 3px 6px -2px rgba(205,201,201,0.75);
				.location-box{
					.black{
						display: flex;
					}
					.white,
					.locat-text,
					.arrow{
						display: none;
					}
				}
				.search-box{
					background-color: #f6f6f6;
					position: absolute;
					width: 50%;
					left: 80upx;
					bottom: 16upx;
				}
				.top-cate-box{
					padding: 0;
					.inner{
						display: none;
					}
				}
			}
		}
		.content-inner{
			box-sizing: border-box;
			padding: 0 20upx 20upx;
			background-color: #f6f6f6;
			.menu-cont{
				padding-top: 20upx;
			}
			.small-menu-box{
				height: 80upx;
				border-radius: 20upx;
				display: flex;
				align-items: center;
				justify-content: center;
				background-color: #fff;
				.item{
					display: flex;
					align-items: center;
					.img{
						width: 38upx;
						height: 38upx;
						margin-right: 10upx;
					}
					.text{
						font-size: 24upx;
						color: #000;
						font-weight: bold;
					}
				}
				.line{
					width: 2upx;
					height: 34upx;
					background-color: #f7f7f7;
					margin: 0 20upx;
				}
			}
			.nearby-merchants{
				margin-top: 20upx;
				border-radius: 20upx;
				background-color: #ffffff;
				padding: 0 24upx 24upx;
				.title-box{
					display: flex;
					align-items: center;
					justify-content: space-between;
					padding-top: 24upx;
					margin-bottom: 20upx;
					.label{
						font-size: 30upx;
						color: #000;
						font-weight: bold;
					}
					.show-more{
						display: flex;
						align-items: center;
						.text{
							font-size: 24upx;
							color: #000;
						}
						.img{
							width: 24upx;
							height: 24upx;
							margin-left: 10upx;
						}
					}
				}
				.busi-cate{
					display: flex;
					align-items: center;
					.item{
						flex-shrink: 0;
						height: 40upx;
						line-height: 40upx;
						padding: 0 22upx;
						border-radius: 20upx;
						background-color: item;
						font-size: 24upx;
						color: #000;
						margin-right: 20upx;
						background-color: #f6f6f6;
						&:last-child{
							margin-right: 0;
						}
						&.active{
							background-color: #ebf9ec;
							color: #00b52c;
							font-weight: bold;
						}
					}
				}
				.busi-list{
					display: flex;
					align-items: center;
					padding-top: 20upx;
					.item{
						flex-shrink: 0;
						width: 206upx;
						height: 250upx;
						background-color: #fafafa;
						border-radius: 10upx;
						overflow: hidden;
						margin-right: 16upx;
						&:last-child{
							margin-right: 0;
						}
						.adver-box{
							width: 100%;
							height: 136upx;
							position: relative;
							.adver{
								width: 100%;
								height: 100%;
							}
							.logo{
								width: 86upx;
								height: 86upx;
								border-radius: 50%;
								position: absolute;
								left: 50%;
								transform: translateX(-50%);
								bottom: -16upx;
							}
						}
						.info-box{
							padding: 0 10upx;
							display: flex;
							flex-direction: column;
							align-items: center;
							.name{
								max-width: 100%;
								text-align: center;
								font-size: 24upx;
								color: #000;
								line-height: 1;
								margin-top: 30upx;
								margin-bottom: 10upx;
							}
							.securit{
								max-width: 100%;
								width: auto;
								box-sizing: border-box;
								height: 32upx;
								line-height: 32upx;
								font-size: 22upx;
								color: #df393a;
								border: 1px solid #df393a;
								padding: 0 8upx;
								border-radius: 8upx;
							}
							.time{
								box-sizing: border-box;
								max-width: 100%;
								height: 32upx;
								line-height: 32upx;
								font-size: 22upx;
								color: #3d8de8;
								padding: 0 8upx;
								background-color: #ebeffe;
								border-radius: 8upx;
							}
						}
					}
				}
			}
			
			.goods-cate{
				display: flex;
				align-items: center;
				justify-content: space-between;
				padding: 0 10upx;
				.item{
					flex-shrink: 0;
					height: 120upx;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					.label{
						font-size: 28upx;
						color: #000;
						line-height: 1;
						font-weight: bold;
						margin-bottom: 8upx;
					}
					.text{
						font-size: 24upx;
						color: #969696;
						height: 38upx;
						line-height: 38upx;
						padding: 0 16upx;
						border-radius: 19upx;
					}
					&.active{
						.label{
							color: #28e036;
						}
						.text{
							background-color: #28e036;
							color: #fff;
						}
					}
				}
				.line{
					flex-shrink: 0;
					width: 2upx;
					height: 40upx;
					background-color: #e4e4e4;
					margin: 0 30upx;
				}
			}
			.sub-cate{
				padding: 20upx 20upx 4upx;
				background-color: #fff;
				border-radius: 20upx;
				display: flex;
				flex-wrap: wrap;
				background-color: #fff;
				.item{
					width: 23.5%;
					height: 56upx;
					line-height: 56upx;
					border-radius: 28upx;
					background-color: #f6f6f6;
					margin-right: 2%;
					margin-bottom: 16upx;
					text-align: center;
					font-size: 24upx;
					color: #5c5c5c;
					&:nth-child(4n) {
						margin-right: 0;
					}
					&.active{
						background-color: #e5f9ee;
						color: #00d247;
						font-weight: bold;
					}
				}
			}
			
		}
	}
</style>
