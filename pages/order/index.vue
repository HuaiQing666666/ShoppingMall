<template>
	<view class="content">
		<!-- 无数据 -->
		<view v-if="orderList.length == 0" class="empty-order">
			<image src="../../static/images/icon_order_no.png" mode="heightFix"></image>
			<text class="text">暂无订单，快去下单吧~</text>
			<view class="btn">去逛逛</view>
		</view>
		<!-- 订单列表 -->
		<view  v-if="orderList.length > 0"  class="order-list">
			<view v-for="(item,index) in orderList" :key="index" class="item" @click="showDetail">
				<div class="store-info">
					<view class="img-box">
						<image src="../../static/logo.png" mode=""></image>
					</view>
					<view class="info-det">
						<view class="top-cont">
							<view class="title ellipsis">这里是门店名称这里是门店名称这里是门店名称</view>
							<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
							<view class="status">已完成</view>
						</view>
						<view class="store-status gray">门店休息中</view>
					</view>
				</div>
				<!-- 优惠券 -->
				<view class="order-coupon">
					<view class="coup-item">领10元券</view>
					<view class="coup-item">领18元券</view>
					<view class="coup-item">领50元叠加券</view>
				</view>
				<!-- 商品 -->
				<view class="order-goods">
					<scroll-view class="img-scroll-box" scroll-x="true" >
						<view class="img-box">
							<image v-if="index == 0" v-for="(item,g) in 6" :key="j" src="../../static/logo.png" mode="heightFix"></image>
							<image v-if="index == 1" v-for="(item,g) in 3" :key="j" src="../../static/logo.png" mode="heightFix"></image>
						</view>
					</scroll-view>
					<view :class="index ==0?'total-num more':'total-num'">共3件</view>
				</view>
				<!-- 取货方式、价格 -->
				<view class="other-info">
					<view class="mode-time">
						<view class="mode">到点自提</view>
						<view class="time">2022-07-09 22:48</view>
					</view>
					<view class="price">￥67.2</view>
				</view>
				<!-- 按钮 -->
				<view class="btn-box">
					<view class="btn buy">再次购买</view>
				</view>
			</view>
		</view>
		<!-- 猜你喜欢 -->
		<view class="like-box">
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
</template>

<script>
	export default {
		data() {
			return {
				orderList: [1,2]
			}
		},
		methods: {
			showDetail() {
				uni.navigateTo({
					url: './orderDetail'
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		background: #f6f6f6;
	}
</style>
<style scoped lang="scss">
	.content{
		padding: 20upx;
		.empty-order{
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			padding: 30upx 0 40upx;
			image{
				height: 100upx;
			}
			.text{
				font-size: 28upx;
				color: #333;
				margin: 40upx 0;
			}
			.btn{
				height: 70upx;
				line-height: 70upx;
				padding: 0 40upx;
				font-size: 24upx;
				border-radius: 35upx;
				color: #fff;
				background-color: #35d861;
			}
		}
		.order-list{
			.item{
				background-color: #fff;
				border-radius: 10upx;
				overflow: hidden;
				margin-bottom: 16upx;
				padding: 30upx 20upx;
				.store-info{
					display: flex;
					align-items: center;
					.img-box{
						flex-shrink: 0;
						width: 80upx;
						height: 80upx;
						border-radius: 10upx;
						overflow: hidden;
						background-color: #fff;
						border: 2upx solid #e9e9e9;
						margin-right: 20upx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.info-det{
						width: calc(100% - 100upx);
						display: flex;
						flex-direction: column;
						align-items: flex-start;
						.top-cont{
							width: 100%;
							display: flex;
							align-items: center;
							.title{
								width: 75%;
								font-size: 28upx;
								color: #000;
								font-weight: bold;
							}
							.arrow{
								height: 22upx;
								margin-right: 30upx;
								margin-left: 10upx;
							}
							.status{
								font-size: 26upx;
								color: #333;
							}
						}
						.store-status{
							height: 34upx;
							line-height: 34upx;
							padding: 0 10upx;
							border-radius: 4upx;
							background-color: #686868;
							font-size: 20upx;
							color: #fff;
							margin-top: 10upx;
						}
					}
				}
				
				.order-coupon{
					margin-top: 20upx;
					padding-left: 100upx;
					display: flex;
					flex-wrap: wrap;
					.coup-item{
						height: 34upx;
						line-height: 34upx;
						border: 2upx solid #e7d2d0;
						padding: 0 14upx;
						font-size: 22upx;
						color: #da1b1e;
						border-radius: 8upx;
						position: relative;
						margin-right: 12upx;
						margin-bottom: 10upx;
						&::before{
							content: "";
							position: absolute;
							left: -15upx;
							top: 50%;
							background-color: #fff;
							transform: translateY(-50%);
							width: 18upx;
							height: 18upx;
							border: 2upx solid #e7d2d0;
							border-radius: 18upx;
							clip-path: polygon(50% 0%, 100% 0%, 100% 3600%, 50% 50%);
						}
						&::after{
							content: "";
							position: absolute;
							right: -15upx;
							top: 25%;
							background-color: #fff;
							transform: translateY(-50%);
							width: 18upx;
							height: 18upx;
							border: 2upx solid #e7d2d0;
							border-radius: 18upx;
							clip-path: polygon(50% 0%, 100% 0%, 100% 3600%, 50% 50%);
							transform: rotate(180deg);
						}
					}
				}
				.order-goods{
					display: flex;
					align-items: center;
					justify-content: space-between;
					margin-top: 20upx;
					.img-scroll-box{
						width: calc(100% - 100upx);
					}
					.img-box{
						width: 100%;
						display: flex;
						align-items: center;
						image{
							flex-shrink: 0;
							height: 90upx;
							margin-right: 20upx;
						}
					}
					.total-num{
						width: 100upx;
						height: 90upx;
						text-align: center;
						line-height: 90upx;
						flex-shrink: 0;
						font-size: 26upx;
						color: #989898;
						&.more{
							box-shadow: -8upx 0px 5upx -4upx rgba(205,203,203,0.3);
						}
					}
				}
				.other-info{
					display: flex;
					align-items: center;
					justify-content: space-between;
					margin-top: 20upx;
					.mode-time{
						display: flex;
						align-items: center;
						.mode{
							height: 34upx;
							line-height: 34upx;
							padding: 0 10upx;
							border-radius: 8upx;
							font-size: 22upx;
							color: #006fee;
							border: 2upx solid #006fee;
							margin-right: 10upx;
						}
						.time{
							font-size: 20upx;
							color: #7c7c7c;
						}
					}
					.price{
						font-size: 28upx;
						color: #000;
						font-weight: bold;
					}
				}
				.btn-box{
					display: flex;
					align-items: center;
					justify-content: flex-end;
					margin-top: 20upx;
					.btn{
						width: 200upx;
						height: 60upx;
						line-height: 60upx;
						text-align: center;
						border-radius: 30upx;
						border: 2upx solid #e4e4e4;
						font-size: 26upx;
						color: #000;
					}
				}
			}
		}
	}
</style>
