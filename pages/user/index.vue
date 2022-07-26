<template>
	<scroll-view
		:scroll-top="userScrollTop"
		scroll-y="true" 
		class="content" 
		@scroll="userScroll">
		<view class="top-cont">
			<view :class="fixedTop?'inner fixed':'inner'">
				<!-- 状态栏 -->
				<view :class="fixedTop?'status-bar white-bg':'status-bar'" :style="{height: statusBarHeight +'px'}"></view>
				<view :class="fixedTop?'top-title-box show':'top-title-box'">我的</view>
			</view>
			<!-- 用于顶部固定定位后占位 -->
			<view :class="fixedTop?'seat show':'seat'" :style="{height: statusBarHeight +'px'}"></view>
			<view class="user-info">
				<image class="head" src="../../static/logo.png" mode="aspectFill"></image>
				<view class="inner">
					
					<view class="name-box">
						<text class="name">jd_kdskkdsdmkV</text>
						<view class="set-msg">
							<image src="../../static/images/icon_set.png" mode="aspectFill"></image>
							<view class="img-box">
								<image src="../../static/images/icon_msg.png" mode="aspectFill"></image>
							</view>
						</view>
					</view>
					<view class="phone">
						<text class="num">131****8989</text>
						<image src="../../static/images/icon_edit.png" mode=""></image>
					</view>
				</view>
			</view>
			<!-- 我的钱包 -->
			<view class="my-wallet">
				<view class="wallet">
					<image src="../../static/images/icon_wallet.png" mode=""></image>
					<text class="text">我的钱包</text>
				</view>
				<image class="line" src="../../static/images/img_line.png" mode="heightFix"></image>
				<view class="inner">
					<view class="item">
						<text class="num">0</text>
						<text class="label">红包</text>
					</view>
					<view class="item">
						<text class="num">3</text>
						<text class="label">优惠券</text>
					</view>
					<view class="item">
						<text class="num">0</text>
						<text class="label">鲜豆</text>
					</view>
					<view class="item">
						<text class="num">0</text>
						<text class="label">激活白条</text>
					</view>
				</view>
			</view>
		</view>
		<view class="cont-inner">
			<!-- 功能服务 -->
			<view class="menu-box">
				<view class="title">功能服务</view>
				<view class="menu-inner">
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的关注</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的评价</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的地址</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">V+会员</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">签到有惊喜</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">售后退款</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">客服与帮助</text>
					</view>
				</view>
			</view>
			<!-- 金融福利 -->
			<view class="menu-box">
				<view class="title">金融福利</view>
				<view class="menu-inner">
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的关注</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的评价</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的地址</text>
					</view>
				</view>
			</view>
			<!-- 更多推荐 -->
			<view class="menu-box">
				<view class="title">更多推荐</view>
				<view class="menu-inner">
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的关注</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的评价</text>
					</view>
					<view class="item">
						<image class="img" src="../../static/images/icon_signin.png" mode="heightFix"></image>
						<text class="label">我的地址</text>
					</view>
				</view>
			</view>
			<!-- 猜你喜欢 -->
			<view class="like-box" style="margin-top: 20upx;">
				<image src="../../static/images/icon_like_l.png" mode="widthFix"></image>
				<view class="text">猜你喜欢</view>
				<image src="../../static/images/icon_like_r.png" mode="widthFix"></image>
			</view>
			<!-- 商品推荐列表 -->
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
	export default {
		data() {
			return {
				userScrollTop: 0,
				fixedTop: false, // 是否固定头部
				statusBarHeight: uni.getStorageSync('statusBarHeight'),
			}
		},
		methods: {
			userScroll(e) {
				if(e.detail.scrollTop >= 10) {
					this.fixedTop = true
				} else {
					this.fixedTop = false
				}
			},
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
		background: #f6f6f6;
	}
</style>
<style scoped lang="scss">
	.content{
		height: 100%;
	}
	.top-cont{
		height: 370upx;
		position: relative;
		&::after{
			content: '';
			width: 140%;
			height: 370upx;
			position: absolute;
			z-index: -1;
			left: -20%;
			top: 0;
			border-radius: 0 0 50% 50%;
			background: linear-gradient(160deg,#5de573, #03cf3a);
		}
		.inner.fixed{
			width: 100%;
			position: fixed;
			top: 0;
			left: 0;
			z-index: 999;
		}
		.seat{
			display: none;
			&.show{
				display: block;
			}
		}
		.status-bar.white-bg {
			background-color: #fff;
		}
		.top-title-box{
			height: 88upx;
			line-height: 88upx;
			text-align: center;
			background-color: #fff;
			font-size: 28upx;
			color: #000;
			display: none;
			&.show{
				display: block;
			}
		}
	
		.user-info{
			padding: 20upx;
			display: flex;
			align-items: center;
			margin-top: 88upx;
			padding-top: 0;
			.head{
				width: 100upx;
				height: 100upx;
				border-radius: 50%;
				overflow: hidden;
				margin-right: 20upx;
			}
			.inner{
				flex: 1;
				height: 90upx;
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				.name-box{
					display: flex;
					align-items: center;
					justify-content: space-between;
					.name{
						font-size: 32upx;
						color: #fff;
						font-weight: bold;
						line-height: 1;
					}
					.set-msg{
						display: flex;
						align-items: center;
						justify-content: flex-end;
						padding-right: 20upx;
						.img-box{
							position: relative;
						}
						image{
							width: 40upx;
							height: 40upx;
							margin-left: 20upx;
						}
					}
				}
				.phone{
					display: flex;
					align-items: center;
					.num{
						font-size: 24upx;
						color: #fff;
					}
					image{
						width: 28upx;
						height: 28upx;
						margin-left: 20upx;
					}
				}
			}
		}
		.my-wallet{
			width: calc(100% - 40upx);
			background-color: #fff;
			border-radius: 20upx;
			height: 160upx;
			margin: 0 auto;
			display: flex;
			align-items: center;
			.wallet{
				display: flex;
				flex-direction: column;
				align-items: center;
				margin-left: 36upx;
				image{
					width: 42upx;
					height: 42upx;
					margin-bottom: 10upx;
				}
				.text{
					font-size: 22upx;
					color: #000;
				}
			}
			.line{
				height: 110upx;
				margin-left: 10upx;
			}
			.inner{
				flex: 1;
				display: flex;
				align-items: center;
				justify-content: space-around;
				.item{
					min-width: 96upx;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					.num{
						font-size: 32upx;
						color: #000;
						font-weight: bold;
						margin-bottom: 20upx;
						line-height: 1;
					}
					.label{
						font-size: 24upx;
						color: #000;
						line-height: 1;
					}
				}
			}
		}
	}
	.cont-inner{
		padding: 90upx 20upx 20upx;
		.menu-box{
			background-color: #fff;
			border-radius: 20upx;
			margin-top: 20upx;
			padding: 0 20upx 20upx;
			.title{
				height: 90upx;
				line-height: 90upx;
				font-size: 32upx;
				color: #000;
				font-weight: bold;
			}
			.menu-inner{
				display: flex;
				flex-wrap: wrap;
				.item{
					width: 25%;
					height: 120upx;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					.img{
						height: 44upx;
						margin-bottom: 20upx;
					}
					.label{
						font-size: 24upx;
						color: #000;
					}
				}
			}
		}
	}
</style>
