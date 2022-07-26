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
				<image class="back" src="../../static/images/icon_back_b.png" mode="heightFix" @click="goBack"></image>
				<text class="text">商品详情</text>
			</view>
		</view>
		<!-- 轮播图 -->
		<swiper class="phonto-swiper" circular indicator-color="#fff" indicator-active-color="#0dc64d" :indicator-dots="true" :autoplay="true" :interval="2000" :duration="500">
			<swiper-item v-for="(item,index) in 2" :key="index">
				<image class="phonto" src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-aa63ef669debe3251bb32f09252e654f_r.jpg&refer=http%3A%2F%2Fpic4.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1660398671&t=29aeda563ebd1bdacac7df0374cd3246" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 商品信息 -->
		<view class="goods-info">
			<view class="title">Apple iPhone 13 Pro Max 支持移动联通电信5G 双卡双待手机</view>
			<view class="price-btn">
				<view class="price">￥9777</view>
				<view class="btn-box">
					<view v-if="shoppingCar > 0" class="add-sub-box">
						<view class="sub" @click="subGoods">-</view>
						<view class="text">{{ shoppingCar }}</view>
						<view class="add" @click="addGoods($event,1)">+</view>
					</view>
					<view v-if="shoppingCar == 0" class="btn add" @click="addGoods($event,1)">加入购物车</view>
					<!-- <view class="btn buy">立即购买</view> -->
				</view>
			</view>
			<!-- 参数等 -->
			<view class="param-box">
				<view class="item">
					<view class="label">上市时间</view>
					<view class="text">2021年9月</view>
				</view>
				<view class="line"></view>
				<view class="item">
					<view class="label">摄像头数量</view>
					<view class="text">后置三摄</view>
				</view>
				<view class="line"></view>
				<view class="item">
					<view class="label">特征特质</view>
					<view class="text">5G</view>
				</view>
			</view>
		</view>
		<!-- 搭配购买 -->
		<view class="collocat-box">
			<view class="title">搭配购买</view>
			<scroll-view scroll-x="true" >
				<view class="collo-goods">
					<view v-for="(item,index) in 5" :key="index" class="item">
						<view class="img-box">
							<image src="../../static/images/car_select.png" mode="heightFix"></image>
						</view>
						<view v-if="index == 1" class="name ellipsis2">华为智选手机</view>
						<view v-else class="name ellipsis2">华为智选手机 Hi nova 9 5G全网通等等等的的呢过到</view>
						<view class="price-btn">
							<view class="price">￥9999</view>
							<view class="btn">+</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 商家信息 -->
		<view class="busi-info">
			<view class="left">
				<image class="busi" src="../../static/images/icon_busi.png" mode=""></image>
				<view class="text">这里是-商家地址商家地址商家</view>
				<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
			</view>
			<view class="right" @click="call">
				<image class="phone" src="../../static/images/icon_phone.png" mode="heightFix"></image>
				<text class="text">联系商家</text>
			</view>
		</view>
		<!-- 商品详情 -->
		<view class="prod-details">
			<view class="title">商品详情</view>
			<view class="det-cont">
				<u-parse :content="content" :selectable="true"></u-parse>
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
				content: `
					<p>露从今夜白，月是故乡明</p>
					<img src="https://cdn.uviewui.com/uview/swiper/2.jpg" />
				`,
				fixedTop: false, // 是否固定头部搜索框
				scrollTop: 0,
				shoppingCar: 0, // 购物车数量
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
			call() {
				uni.makePhoneCall({
					phoneNumber: '114',
					success:function(){
						console.log('拨打电话成功');
					},
					fail() {
						console.log('打电话失败了');
					}
				})
			},
			// 添加购物车
			// e 是位置等参数 id是为了重复使用点击位置点  需要保证id不重复
			addGoods(e,id) {
				this.$refs.inCart.addToCart(e,id);
				this.shoppingCar += 1
				console.log(this.shoppingCar)
			},
			// 购物车减
			subGoods() {
				this.shoppingCar -= 1
				if(this.shoppingCar < 0) {
					this.shoppingCar = 0
				}
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
			background-color: rgba(255, 255, 255, 0);
			&.fixed{
				background-color: rgba(255, 255, 255, 1);
				.inner{
					.back{
						display: block;
					}
					.text{
						display: block;
					}
				}
			}
			.inner{
				height: 88upx;
				line-height: 88upx;
				display: flex;
				align-items: center;
				justify-content: center;
				padding: 0 30upx;
				position: relative;
				.back{
					width: 34upx;
					height: 34upx;
					margin-right: 10upx;
					position: absolute;
					top: 50%;
					transform: translateY(-50%);
					left: 30upx;
				}
				.text{
					font-size: 28upx;
					color: #000;
					display: none;
				}
			}
		}
		.phonto-swiper{
			height: 750upx;
			.phonto{
				width: 100%;
				height: 100%;
			}
		}
		.goods-info{
			background-color: #fff;
			border-radius: 0 0 20upx 20upx;
			padding: 30upx 20upx;
			overflow: hidden;
			.title{
				font-size: 36upx;
				color: #000;
				font-weight: bold;
			}
			.price-btn{
				margin-top: 30upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.price{
					font-size: 44upx;
					color: #ff1d1f;
					font-weight: bold;
				}
				.btn-box{
					display: flex;
					align-items: center;
					.add-sub-box{
						display: flex;
						align-items: center;
						justify-content: center;
						.sub{
							width: 40rpx;
							height: 40rpx;
							line-height: 34rpx;
							text-align: center;
							border-radius: 50%;
							border: 2upx solid #13d34b;
							font-size: 24rpx;
							color: #13d34b;
						}
						.text{
							font-size: 28upx;
							color: #000;
							margin: 0 30upx;
						}
						.add{
							width: 40rpx;
							height: 40rpx;
							line-height: 36rpx;
							text-align: center;
							border-radius: 50%;
							background-color: #13d34b;
							font-size: 24rpx;
							color: #fff;
						}
					}
					.btn{
						width: 170upx;
						height: 66upx;
						line-height: 66upx;
						border-radius: 33upx;
						text-align: center;
						font-size: 24upx;
						color: #fff;
						margin-left: 16upx;
						&:first-child{
							margin-left: 0;
						}
						&.add{
							background: linear-gradient(to right, #00ca20,#03bd36);
						}
						&.buy{
							background: linear-gradient(to right, #ff8a3a,#fd5516);
						}
					}
				}
			}
			.param-box{
				display: flex;
				align-items: center;
				justify-content: space-around;
				padding-top: 30upx;
				border-top: 2upx solid #f5f5f5;
				margin-top: 30upx;
				.item{
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					.label{
						font-size: 24upx;
						color: #000;
						line-height: 1;
					}
					.text{
						font-size: 24upx;
						color: #949494;
						line-height: 1;
						margin-top: 15upx;
					}
				}
				.line{
					width: 2upx;
					height: 70upx;
					background-color: #f5f5f5;
				}
			}
		}
		.collocat-box{
			padding: 40upx 20upx;
			background-color: #fff;
			margin-top: 20upx;
			border-radius: 20upx;
			.title{
				font-size: 28upx;
				color: #000;
				font-weight: bold;
				margin-bottom: 30upx;
			}
			.collo-goods{
				display: flex;
				align-items: center;
				.item{
					width: 200upx;
					margin-right: 20upx;
					.img-box{
						width: 200upx;
						height: 200upx;
						border-radius: 8upx;
						background-color: #fafafa;
						image{
							height: 100%;
						}
					}
					.name{
						min-height: 60upx;
						font-size: 22upx;
						color: #000;
						margin-top: 10upx;
					}
					.price-btn{
						margin-top: 10upx;
						display: flex;
						align-items: center;
						justify-content: space-between;
						.price{
							font-size: 22upx;
							color: #f70000;
							font-weight: bold;
						}
						.btn{
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
		.busi-info{
			height: 120upx;
			background-color: #fff;
			border-radius: 20upx;
			padding: 0 20upx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			margin-top: 20upx;
			.left{
				display: flex;
				align-items: center;
				.busi{
					width: 30upx;
					height: 30upx;
					margin-right: 10upx;
				}
				.text{
					font-size: 24upx;
					color: #000;
					font-weight: bold;
				}
				.arrow{
					height: 20upx;
					margin-left: 10upx;
				}
			}
			.right{
				display: flex;
				align-items: center;
				.phone{
					height: 28upx;
				}
				.text{
					font-size: 26upx;
					color: #333;
					margin-left: 10upx;
				}
			}
		}
		.prod-details{
			padding: 40upx 20upx;
			background-color: #fff;
			margin-top: 20upx;
			border-radius: 20upx;
			margin-bottom: 160upx;
			.title{
				font-size: 28upx;
				color: #000;
				font-weight: bold;
				margin-bottom: 30upx;
			}
			.det-cont{
				font-size: 32rpx;
				color: $u-content-color;
				line-height: 1.6;
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
