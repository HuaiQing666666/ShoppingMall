<template>
	<scroll-view
		:scroll-top="scrollTop"
		scroll-y="true" 
		class="content" 
		@scroll="scroll">
		<view :class="fixedTop?'top-cont fixed':'top-cont'">
			<!-- 状态栏 -->
			<view class="status-bar" :style="{height: statusBarHeight +'px'}"></view>
			<view class="inner">
				<image class="back white" src="../../static/images/icon_back_w.png" mode="heightFix" @click="goBack"></image>
				<image class="back black" src="../../static/images/icon_back_b.png" mode="heightFix" @click="goBack"></image>
				<view class="search-box">
					<image class="img" src="../../static/images/icon_search.png" mode="heightFix"></image>
					<text class="text">店内104件商品</text>
				</view>
				<!-- 关注 -->
				<view class="follow-box" @click="followChange">
					<image v-if="!isFollow" src="../../static/images/icon_follow.png" mode="aspectFill"></image>
					<text v-if="!isFollow" class="text">关注</text>
					<text v-if="isFollow" class="text">已关注</text>
				</view>
			</view>
		</view>
		
		<view class="content-inner">
			<view class="content-item">
				<!-- 背景图 -->
				<image class="bg" src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg95.699pic.com%2Fphoto%2F40021%2F1745.jpg_wh300.jpg&refer=http%3A%2F%2Fimg95.699pic.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1660189141&t=a58f627c813f1c676e1c6d66f068aa41" mode="aspectFill"></image>

				<view class="status-bar" :style="{height: statusBarHeight +'px'}"></view>
				<!-- 店铺信息 -->
				<view class="busi-info">
					<view class="inner">
						<view class="img-box">
							<image src="../../static/logo.png" mode="aspectFill"></image>
						</view>
						<view class="info-det">
							<view class="title ellipsis">Apple授权-尚派中海环宇城</view>
							<view class="time-box">
								<text class="time">明日10:00起送</text>
								<text class="tag">免运费</text>
							</view>
						</view>
					</view>
					<!-- 优惠券 -->
					<scroll-view scroll-x="true" >
						<view class="coupon-list">
							<view v-for="(item,index) in 6" :key="index" :class="index==0?'item receiv':'item'">
								<view class="left">
									<view class="price">￥50</view>
									<view class="name">限品券</view>
								</view>
								<view v-if="index == 0" class="right">去使用</view>
								<view v-else class="right">领取</view>
							</view>
						</view>
					</scroll-view>
				</view>
			</view>
			<!-- tab切换 -->
			<u-sticky :offset-top="88+statusBarHeight">
				<view class="tabs-box">
					<view :class="activeTab ==1?'item active':'item'" @click="tabChange(1)">首页</view>
					<view :class="activeTab ==2?'item active':'item'" @click="tabChange(2)">全部商品</view>
				</view>
			</u-sticky>
			<!-- 首页 -->
			<view v-if="activeTab == 1" class="busi-home">
				<scroll-view scroll-x="true" >
					<view class="cate-list">
						<view v-for="(item,index) in 8" :key="index" class="item">
							新品上市
						</view>
					</view>
				</scroll-view>
				<!-- 图片轮播 -->
				<swiper class="phonto-swiper" circular indicator-color="#fff" indicator-active-color="#0dc64d" :indicator-dots="true" :autoplay="false" :interval="2000" :duration="500">
					<swiper-item v-for="(item,index) in 2" :key="index">
						<image class="phonto" src="../../static/logo.png" mode=""></image>
					</swiper-item>
				</swiper>
				<!-- 商品列表 -->
				<view v-for="(item,index) in 3" :key="index" class="busi-goods">
					<view class="title-box">
						<text class="label">新品上市</text>
						<view class="right">
							<text class="text">更多</text>
							<image class="arrow" src="../../static/images/icon_arrow_r.png" mode=""></image>
						</view>
					</view>
					<view class="goods-inner">
						<view v-for="(goods,j) in 6" :key="j" class="item" @tap="showDetail">
							<view class="img-box">
								<image src="../../static/logo.png" mode="heightFix"></image>
								<!-- 活动 -->
								<view class="act-title">预估到手</view>
								<view class="act-num">￥4229</view>
							</view>
							<view class="info-box">
								<view class="info-title">
									<view v-if="j == 0" class="tag">新品</view>
									<view class="title ellipsis">商品名称名称很hence或或或或付多或多所军付</view>
								</view>
								<!-- 规格 -->
								<view v-if="j == 0" class="specs">
									<view class="specs-item">128GB</view>
									<view class="specs-item">后置三摄</view>
								</view>
								<view v-else class="specs-text ellipsis">文字描述文字描述文字描述文字描述</view>
							</view>
							<view class="price-box">
								<view class="price">
									<text class="num">￥4399</text>
									<text class="unit">起</text>
								</view>
								<view class="add-btn">+</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<!-- 全部商品 -->
			<view v-if="activeTab == 2" class="all-products">
				<scroll-view class="prod-cate-scroll" scroll-y="true">
					<view class="prod-cate">
						<view 
							v-for="(item,index) in prodCate" :key="index" 
							:class="prodActiveCate == index?'cate-inner active':'cate-inner'"
							@click="prodCateChose(index)"
						>
							<view class="inner">
								<text class="text">{{ item.name }}</text>
								<image v-if="item.children.length > 0" class="arrow" src="../../static/images/icon_arrow_b_d.png" mode=""></image>
							</view>
							<view v-if="item.children.length > 0" class="sub-cate-box">
								<view v-for="(sub,j) in item.children" :key="j" class="sub-item">
									{{ sub.name }}
								</view>
							</view>
						</view>
					</view>
				</scroll-view>
				<scroll-view class="prod-goods-scroll" scroll-y="true" @scroll="goodsScroll">
					<!-- 筛选条件 -->
					<view class="screen-box">
						<view class="screen">
							<text class="text">综合排序</text>
							<image class="arrow" src="../../static/images/icon_arrow_b_d.png" mode=""></image>
						</view>
						<view class="screen">
							<text class="text">减免运费</text>
						</view>
					</view>
					<!-- 商品列表 -->
					<view class="prod-list">
						<view v-for="(item,index) in goodsList" :key="index" class="item" @tap="showDetail">
							<view class="img-box">
								<image src="../../static/images/car_select.png" mode="heightFix"></image>
							</view>
							<view class="prod-info">
								<view class="title ellipsis2">{{ item.name + index }}</view>
								<view class="sub-title">月售12 好评100%</view>
								<view class="specs-box">
									<view class="specs-item">128G</view>
									<view class="specs-item">后置三摄</view>
									<view class="specs-item">5G</view>
								</view>
								<view class="activity-box">
									<view class="act-item">秒杀3.92折扣限99份</view>
								</view>
								<view class="prod-price-box">
									<view class="left">
										<view class="new">￥3.48</view>
										<view class="old">￥8.9</view>
									</view>
									<view class="add-btn add-to-car" @tap.stop="addGoods($event,item.id)">+</view>
								</view>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
		
		<view  :style="{height: bottomBlackLineHeight +'rpx'}"></view>
		<!-- 底部购物车显示 -->
		<view class="bottom-box" :style="{paddingBottom: bottomBlackLineHeight +'rpx'}">
			<view :class="shoppingCar>0?'empty-car has-goods':'empty-car'" id="cart">
				<view class="left">
					<view class="img-box">
						<u-badge max="99" :value="shoppingCar"></u-badge>
						<image class="car" src="../../static/images/icon_shopcar_white.png" mode=""></image>
					</view>
					<text class="label">购物车是空的</text>
				</view>
				<view class="right" @click="confirmOrder">去结算</view>
			</view>
		</view>
		<!-- 只需要绑定购物车位置即可 -->
		<flyInCart ref="inCart" :cartBasketRect="cartBasketRect"></flyInCart>
	</scroll-view>
</template>

<script>
	//  加入购物车动画组件
	import flyInCart from '@/components/ar-flyCart/flyInCart.vue'
	export default {
		components:{
			flyInCart
		},
		data() {
			return {
				statusBarHeight: uni.getStorageSync('statusBarHeight'),
				bottomBlackLineHeight: uni.getStorageSync('bottomBlackLineHeight'),
				fixedTop: false, // 是否固定头部搜索框
				scrollTop: 0,
				isFollow: false, // 是否关注
				activeTab: 1, // 当前展示的页面：1、首页，2、全部商品
				shoppingCar: 0, // 购物车
				// 商品分类
				prodCate:[
					{
						name: '秒杀',
						children: []
					},
					{
						name: '数码科技',
						children: [
							{
								name: '分类五个字'
							},
							{
								name: '分类五个字'
							},
							{
								name: '分类五个字'
							}
						]
					},
					{
						name: '数码科技',
						children: []
					},
					{
						name: '数码科技',
						children: []
					},
					{
						name: '数码科技',
						children: []
					},
					{
						name: '数码科技',
						children: []
					},
					{
						name: '数码科技',
						children: []
					},
					{
						name: '数码科技',
						children: []
					},
					{
						name: '数码科技',
						children: []
					}
				],
				prodActiveCate: 0, // 全部商品选中的分类
				goodsList: [
					{id:1,name:'商品名称'},
					{id:2,name:'商品名称'},
					{id:3,name:'商品名称'},
					{id:4,name:'商品名称'},
					{id:5,name:'商品名称'},
					{id:6,name:'商品名称'},
				],
				// 购物车位置数据
				cartBasketRect:{},
			}
		},
		onReady() {
			const self = this
			let q = uni.createSelectorQuery()
			//获取购物车位置
			setTimeout(function(){
				q.select('#cart').boundingClientRect(data => {
					self.cartBasketRect = data
				}).exec();
			},100)
		},
		methods: {
			scroll(e) {
				if(e.detail.scrollTop >= 10) {
					this.fixedTop = true
				} else {
					this.fixedTop = false
				}
			},
			// 返回上一页
			goBack() {
				uni.navigateBack({
					delta:1,
				})
			},
			// 关注
			followChange() {
				this.isFollow = !this.isFollow
				if(this.isFollow) {
					uni.showToast({
						title: '关注成功'
					})
				} else {
					uni.showToast({
						title: '已取消关注'
					})
				}
			},
			// tab切换
			tabChange(index) {
				this.activeTab = index
			},
			// 全部商品分类选择
			prodCateChose(index){
				this.prodActiveCate = index
			},
			// 商品详情
			showDetail() {
				uni.navigateTo({
					url: './goodsDetail'
				})
			},
			// 添加购物车
			// e 是位置等参数 id是为了重复使用点击位置点  需要保证id不重复
			addGoods(e,id) {
				this.$refs.inCart.addToCart(e,id);
				this.shoppingCar += 1
			},
			// 调用是因为 重复使用了点击动画位置 保证不抖动。 不传参调用即清空点击点
			goodsScroll() {
				this.$refs.inCart.addToCart();
			},
			// 确认订单
			confirmOrder() {
				uni.navigateTo({
					url: './confirmOrder'
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
		background-color: #f8f8f8;
	}
</style>
<style scoped lang="scss">
	.content{
		height: 100%;
		position: relative;
		.top-cont{
			width: 100%;
			transition: all .5s;
			position: fixed;
			top: 0;
			left: 0;
			z-index: 999;
			&.fixed{
				background-color: #fff;
				.inner{
					.back.white{
						display: none;
					}
					.back.black{
						display: block;
					}
					.text{
						color: #000;
					}
					.search-box{
						background-color: #f6f6f6;
					}
					.follow-box{
						background-color: #f6f6f6;
					}
				}
			}
			.inner{
				height: 88upx;
				line-height: 88upx;
				display: flex;
				align-items: center;
				padding-left: 30upx;
				.back{
					width: 34upx;
					height: 34upx;
					margin-right: 10upx;
					transition: all .5s;
					&.black{
						display: none;
					}
				}
				.text{
					font-size: 28upx;
					color: #fff;
				}
				.search-box{
					width: 300upx;
					height: 56upx;
					line-height: 56upx;
					display: flex;
					align-items: center;
					background-color: #fff;
					border-radius: 28upx;
					padding-left: 20upx;
					.img{
						height: 30upx;
						margin-right: 12upx;
					}
					.text{
						font-size: 24upx;
						color: #6d6d6d;
						line-height: 1;
					}
				}
				.follow-box{
					width: 126upx;
					height: 56upx;
					display: flex;
					align-items: center;
					justify-content: center;
					background-color: rgba(255, 255, 255, .9);
					border-radius: 28upx;
					margin-left: 24upx;
					image{
						width: 28upx;
						height: 28upx;
						margin-right: 4upx;
					}
					.text{
						font-size: 28upx;
						color: #000;
					}
				}
			}
		}
		.content-inner{
			box-sizing: border-box;
			min-height: 100%;
			padding: 140upx 0 0;
			margin-bottom: 104upx;
			position: relative;
			display: flex;
			flex-direction: column;
			.content-item{
				padding: 0 20upx;
			}
			.bg{
				width: 100%;
				height: 380upx;
				position: absolute;
				top: 0;
				left: 0;
				z-index: -1;
			}
			.busi-info{
				padding: 26upx;
				background-color: #fff;
				border-radius: 20upx;
				position: relative;
				z-index: 1;
				box-shadow: 0px 6upx 10upx 0 rgba(170,167,167,0.5);
				&::after{
					content: "";
					width: calc(100% + 40upx);
					height: 100%;
					background-image: linear-gradient(transparent,#ffffff);
					position: absolute;
					z-index: -1;
					left: -20upx;
					bottom: 0;
				}
				.inner{
					display: flex;
					align-items: center;
					margin-bottom: 24upx;
					.img-box{
						width: 100upx;
						height: 100upx;
						border: 2upx solid #f6f6f6;
						border-radius: 10upx;
						margin-right: 20upx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.info-det{
						width: calc(100% - 120upx);
						height: 100upx;
						display: flex;
						flex-direction: column;
						justify-content: center;
						.title{
							font-size: 40upx;
							color: #000;
							line-height: 1;
						}
						.time-box{
							display: flex;
							align-items: center;
							margin-top: 20upx;
							.time{
								font-size: 24upx;
								color: #707070;
								margin-right: 10upx;
							}
							.tag{
								font-size: 24upx;
								color: #ed1718;
							}
						}
					}
				}
				.coupon-list{
					display: flex;
					align-items: center;
					.item{
						flex-shrink: 0;
						display: flex;
						align-items: center;
						margin-right: 20upx;
						&:last-child{
							margin-bottom: 0;
						}
						&.receiv{
							.left{
								background-color: #fff0f0;
								.price{
									background-color: #ffcac8;
									color: #ed1718;
								}
								.name{
									color: #ed1718;
								}
							}
							.right{
								background-color: #fff0f0;
								color: #ed1718;
							}
						}
						.left{
							height: 46upx;
							line-height: 46upx;
							border-radius: 8upx;
							display: flex;
							align-items: center;
							background-color: #ff5150;
							.price{
								padding: 0 10upx;
								border-radius: 8upx 0 20upx 8upx;
								background-color: #f52c27;
								font-size: 28upx;
								font-weight: bold;
								color: #fff;
							}
							.name{
								flex-shrink: 0;
								padding: 0 10upx;
								font-size: 20upx;
								color: #fff;
							}
						}
						.right{
							padding: 0 10upx;
							height: 46upx;
							line-height: 46upx;
							border-radius: 8upx;
							font-size: 20upx;
							color: #fff;
							background-color: #ff5150;
							border-left: 2upx dashed #fff;
						}
					}
				}
			}
			.tabs-box{
				padding: 40upx 20upx 20upx;
				background-color: #fff;
				position: relative;
				display: flex;
				align-items: center;
				&::after{
					content: "";
					width: calc(100% + 40upx);
					height: 100%;
					background-color: #fff;
					position: absolute;
					z-index: -1;
					left: -20upx;
					bottom: 0;
				}
				.item{
					font-size: 28upx;
					color: #797979;
					margin-right: 60upx;
					&.active{
						font-weight: bold;
						color: #000;
						position: relative;
						&::after{
							content: "";
							width: 40upx;
							height: 8upx;
							border-radius: 4upx;
							background-color: #17d517;
							position: absolute;
							left: 50%;
							transform: translateX(-50%);
							bottom: -12upx;
						}
					}
				}
			}
			.busi-home{
				padding: 0 20upx;
				margin-bottom: 40upx;
				.cate-list{
					display: flex;
					align-items: center;
					position: relative;
					padding-top: 24upx;
					&::after{
						content: "";
						width: calc(100% + 40upx);
						height: 100%;
						background-image: linear-gradient(#ffffff,transparent);
						position: absolute;
						z-index: -1;
						left: -20upx;
						bottom: 0;
					}
					.item{
						flex-shrink: 0;
						width: 168upx;
						height: 66upx;
						line-height: 66upx;
						text-align: center;
						font-size: 24upx;
						color: #545454;
						border-radius: 8upx;
						margin-right: 25upx;
						background-color: #f6f6f6;
					}
				}
				.phonto-swiper{
					height: 230upx;
					margin-top: 40upx;
					.phonto{
						width: 100%;
						height: 100%;
					}
				}
				.busi-goods{
					margin-top: 20upx;
					.title-box{
						padding: 20upx 0;
						display: flex;
						align-items: center;
						justify-content: space-between;
						.label{
							font-size: 34upx;
							color: #272727;
							font-weight: bold;
						}
						.right{
							display: flex;
							align-items: center;
							.text{
								font-size: 24upx;
								color: #1b1b1b;
							}
							.arrow{
								width: 20upx;
								height: 20upx;
								margin-left: 10upx;
							}
						}
					}
					.goods-inner{
						background-color: #fff;
						border-radius: 10upx;
						padding: 20upx 20upx 10upx;
						display: flex;
						flex-wrap: wrap;
						.item{
							width: 32%;
							margin-right: 2%;
							margin-bottom: 20upx;
							border-radius: 10upx;
							&:nth-child(3n){
								margin-right: 0;
							}
							.img-box{
								width: 100%;
								height: 210upx;
								position: relative;
								overflow: hidden;
								display: flex;
								align-items: center;
								justify-content: center;
								background-color: #fafafa;
								image{
									height: 100%;
								}
								.act-title{
									width: 50%;
									height: 42upx;
									line-height: 42upx;
									border-radius: 0 10upx 0 0;
									text-align: center;
									font-size: 24upx;
									color: #d25c45;
									background-color: #fff6e7;
									position: absolute;
									left: 0;
									bottom: 0;
									z-index: 10;
								}
								.act-num{
									width: 50%;
									height: 30upx;
									line-height: 30upx;
									text-align: center;
									font-size: 24upx;
									color: #fff;
									font-weight: bold;
									background-color: #ff3170;
									position: absolute;
									right: 0;
									bottom: 0;
									z-index: 10;
								}
							}
							.info-box{
								width: 100%;
								.info-title{
									width: 100%;
									display: flex;
									align-items: center;
									.tag{
										flex-shrink: 0;
										height: 28upx;
										line-height: 28upx;
										padding: 0 10upx;
										margin-right: 8upx;
										background-image: linear-gradient(to right, #f95553 0%, #ff2122 100%);
										font-size: 20upx;
										color: #fff;
									}
									.title{
										flex: 1;
										font-size: 22upx;
										color: #000;
									}
								}
								.specs{
									display: flex;
									align-items: center;
									margin-top: 4upx;
									.specs-item{
										height: 32upx;
										line-height: 32upx;
										padding: 0 10upx;
										border-radius: 8upx;
										font-size: 18upx;
										color: #6a6a6a;
										background-color: #f6f6f6;
										margin-right: 10upx;
										&:last-child{
											margin-right: 0;
										}
									}
								}
								.specs-text{
									font-size: 22upx;
									color: #000;
								}
							}
							.price-box{
								display: flex;
								align-items: center;
								justify-content: space-between;
								margin-top: 10upx;
								.price{
									display: flex;
									align-items: flex-end;
									.num{
										font-size: 22upx;
										color: #fa2317;
										font-weight: bold;
									}
									.unit{
										font-size: 18upx;
										color: #fa2317;
										line-height: 1.5;
									}
								}
								.add-btn{
									width: 40upx;
									height: 40upx;
									line-height: 40upx;
									text-align: center;
									border-radius: 50%;
									background-color: #13d34b;
									font-size: 24upx;
									color: #fff;
								}
							}
						}
					}
				}
			}
			.all-products{
				flex: 1;
				height: 0;
				display: flex;
				.prod-cate-scroll{
					width: 154upx;
					height: 100%;
				}
				.prod-cate{
					height: 100%;
					width: 154upx;
					background-color: #f4f4f4;
					padding: 10upx 0;
					.cate-inner{
						width: 100%;
						height: 90upx;
						.inner{
							display: flex;
							align-items: center;
							padding-left: 24upx;
						}
						.text{
							line-height: 90upx;
							font-size: 24upx;
							color: #595959;
						}
						&.active{
							// box-sizing: content-box;
							height: auto;
							background-color: #fff;
							box-shadow: 4px 0px 10px 0px rgba(180,180,180,0.51);
							z-index: 99;
							.text{
								color: #000;
							}
							.arrow{
								display: block;
							}
							.sub-cate-box{
								display: block;
							}
						}
						.arrow{
							width: 14upx;
							height: 14upx;
							margin-left: 10upx;
							display: none;
						}
						.sub-cate-box{
							display: none;
							border-top: 2upx solid #cdcdcd;
							.sub-item{
								height: 80upx;
								line-height: 80upx;
								font-size: 22upx;
								color: #595959;
								padding-left: 24upx;
							}
						}
					}
				}
				.prod-goods-scroll{
					width: calc(100% - 154upx);
					height: 100%;
					background-color: #fff;
					.screen-box{
						height: 56upx;
						display: flex;
						align-items: center;
						padding-left: 26upx;
						background-color: #fff;
						.screen{
							display: flex;
							align-items: center;
							margin-right: 30upx;
							.text{
								font-size: 22upx;
							}
							.arrow{
								width: 16upx;
								height: 16upx;
								margin-left: 10upx;
							}
						}
					}
					.prod-list{
						padding: 0 20upx;
						.item{
							padding: 20upx 0;
							border-bottom: 2upx solid #f9f9f9;
							display: flex;
							&:last-child{
								border-bottom: none;
							}
							.img-box{
								width: 150upx;
								height: 150upx;
								background-color: #fafafa;
								border-radius: 8upx;
								margin-right: 20upx;
								image{
									height: 100%;
								}
							}
							.prod-info{
								width: calc(100% - 170upx);
								.title{
									font-size: 28upx;
									color: #000;
									font-weight: bold;
								}
								.sub-title{
									font-size: 20upx;
									color: #5b5b5b;
									margin-top: 10upx;
								}
								.specs-box{
									margin-top: 10upx;
									display: flex;
									align-items: center;
									flex-wrap: wrap;
									.specs-item{
										height: 36upx;
										line-height: 36upx;
										padding: 0 10upx;
										border-radius: 8upx;
										font-size: 20upx;
										color: #5d5d5d;
										background-color: #f4f4f4;
										margin-right: 8upx;
										margin-bottom: 10upx;
									}
								}
								.activity-box{
									display: flex;
									align-items: center;
									flex-wrap: wrap;
									.act-item{
										height: 32upx;
										line-height: 32upx;
										padding: 0 6upx;
										border-radius: 8upx;
										font-size: 20upx;
										color: #fc201f;
										margin-right: 8upx;
										margin-bottom: 10upx;
										border: 2upx solid #f1b1ae;
									}
								}
								.prod-price-box{
									margin-top: 16upx;
									display: flex;
									align-items: center;
									justify-content: space-between;
									.left{
										.new{
											font-weight: bold;
											font-size: 28upx;
											color: #fc201f;
											line-height: 1;
										}
										.old{
											color: #939393;
											font-size: 18upx;
											text-decoration: line-through;
											margin-top: 16upx;
											line-height: 1;
										}
									}
									.add-btn{
										width: 44upx;
										height: 44upx;
										border-radius: 50%;
										line-height: 44upx;
										text-align: center;
										font-size: 28upx;
										color: #fff;
										font-weight: bold;
										background: linear-gradient(to right,#47d970,#04cd37);
									}
								}
							}
						}
					}
				}
			}
			
		}
		.bottom-box{
			width: 100%;
			position: fixed;
			left: 0;
			bottom: 0;
			z-index: 999;
			background-color: #fff;
			.empty-car{
				height: 115upx;
				padding: 0 20upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				&.has-goods{
					.left{
						.img-box{
							background: linear-gradient(#00cb22,#00c030);
						}
						.label{
							color: #fa191f;
							font-weight: bold;
						}
					} 
					.right{
						background: linear-gradient(to right,#43d96b,#03cf3a);
					}
				}
				.left{
					display: flex;
					align-items: center;
					.img-box{
						width: 80upx;
						height: 80upx;
						border-radius: 50%;
						display: flex;
						align-items: center;
						justify-content: center;
						background: linear-gradient(#cdcdcd,#ababab);
						margin-right: 20upx;
						position: relative;
						.car{
							width: 50upx;
							height: 50upx;
						}
						/deep/.u-badge{
							position: absolute;
							top: 0;
							right: -10upx;
						}
					}
					.label{
						font-size: 28upx;
						color: #ababab;
					}
				}
				.right{
					height: 76upx;
					line-height: 76upx;
					border-radius: 38upx;
					padding: 0 30upx;
					font-size: 26upx;
					color: #fbfbfb;
					background: linear-gradient(to right,#cacaca,#acacac);
				}
			}
		}
	}

</style>
