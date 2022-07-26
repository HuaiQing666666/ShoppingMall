<template>
	<view class="content">
		<!-- 订单状态 -->
		<view class="order-status">
			<view class="title-box">
				<text class="status">订单已完成</text>
				<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
			</view>
			<view class="tip">该自提订单如需售后，请联系商家</view>
			<view class="btn-box">
				<view class="btn buy">再次购买</view>
				<view class="btn apply">申请售后</view>
				<button class="btn contact" open-type="contact">联系客服</button>
			</view>
		</view>
		<!-- 提货信息 -->
		<view class="pick-info">
			<view class="title">凭提货码到线下门店取货</view>
			<view class="inner">
				<view class="time">自提时间：7月10日 18:12-22:02</view>
				<view class="shop-address">
					<view class="shop">永辉超市-兰州中海寰宇店(09:00-21:00)</view>
					<view class="address">兰州市安宁区中海寰宇城</view>
				</view>
			</view>
		</view>
		<!-- 商品信息 -->
		<view class="goods-info">
			<view class="shop-name">
				<text class="text">永辉超市-兰州中海寰宇店</text>
				<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
			</view>
			<view class="buy-goods-list">
				<view :class="isShowAllGoods?'show-all inner':'inner'">
					<view v-for="(item,index) in 3" :key="index" class="item">
						<view class="img-box">
							<image src="../../static/logo.png" mode="heightFix"></image>
						</view>
						<view class="info-det">
							<view class="name-box">
								<text class="tag">直降</text>
								<text class="name">商品名称商品名称商品名称商品名</text>
							</view>
							<view class="num-price">
								<view class="num">￥59.9 x 1</view>
								<view class="price">
									<text class="old">￥79.9</text>
									<text class="new">￥59.9</text>
								</view>
							</view>
						</view>
					</view>
				</view>
				<view class="show-more-goods" @click="changShowGoods">
					<text class="text">共3件</text>
					<image :class="isShowAllGoods?'img show-all':'img'" src="../../static/images/icon_arrow_b_d.png" mode="widthFix"></image>
				</view>
			</view>
			<!-- 其他费用 -->
			<view class="fei-item">
				<view class="left">
					<text class="label">包装服务</text>
					<image class="img" src="../../static/images/icon_info.png" mode=""></image>
				</view>
				<view class="price">￥1</view>
			</view>
			<view class="fei-item">
				<view class="left">
					<text class="label">自取调度费</text>
					<image class="img" src="../../static/images/icon_info.png" mode=""></image>
				</view>
				<view class="price">￥5</view>
			</view>
			<view class="fei-item disc">
				<view class="left">
					<text class="tag">优惠</text>
					<text class="label">红包</text>
				</view>
				<view class="price">-￥5</view>
			</view>
			<view class="fei-item disc">
				<view class="left">
					<text class="tag">优惠</text>
					<text class="label">优惠券</text>
				</view>
				<view class="price">-￥15</view>
			</view>
			<!-- 费用合计 -->
			<view class="total-expens">
				<text class="text">共节省</text>
				<text class="num">￥40.4</text>
				<text class="label">实付金额</text>
				<text class="price">￥67.22</text>
			</view>
			<!-- 联系商家 -->
			<view class="call-merch" @click="callMerch">
				<image class="img" src="../../static/images/icon_phone.png" mode=""></image>
				<text class="text">联系商家</text>
			</view>
		</view>
		<!-- 其他信息 -->
		<view class="other-info">
			<view class="title">配送信息</view>
			<view class="item">
				<view class="left">
					<text class="label">配送方式：</text>
					<text class="text">到点自提</text>
				</view>
			</view>
		</view>
		<view class="other-info">
			<view class="title">订单信息</view>
			<view class="item">
				<view class="left">
					<text class="label">订单号码：</text>
					<text class="text">2123123123123123123</text>
				</view>
				<view class="copy-btn" @click="copyOrderSn">复制</view>
			</view>
			<view class="item">
				<view class="left">
					<text class="label">下单时间：</text>
					<text class="text">2022-07-10 12:43:23</text>
				</view>
			</view>
			<view class="item">
				<view class="left">
					<text class="label">支付方式：</text>
					<text class="text">在线支付</text>
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
</template>

<script>
	export default {
		data() {
			return {
				// 订单是否展示所有商品
				isShowAllGoods: false,
			}
		},
		onLoad(options) {
			// 设置顶部导航栏颜色
			uni.setNavigationBarColor({
			  frontColor: '#ffffff',
			  backgroundColor: '#53d25d',
			  animation: {
				duration: 400,
				timingFunc: 'easeIn'
			  }
			})
		},
		methods: {
			changShowGoods() {
				this.isShowAllGoods = !this.isShowAllGoods
			},
			callMerch() {
				uni.makePhoneCall({
					phoneNumber: '114'
				});
			},
			copyOrderSn() {
				uni.setClipboardData({
				    data: '1232131313',
				    success: function () {
						uni.showToast({
							title:'复制成功',
							icon:'none'
						})
				    }
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
		position: relative;
		&::after{
			content: "";
			width: 100%;
			height: 180upx;
			background-color: #53d25d;
			position: absolute;
			top: 0;
			left: 0;
			z-index: -1;
		}
		.order-status{
			box-sizing: border-box;
			height: 254upx;
			background-color: #fff;
			border-radius: 20upx;
			padding-top: 30upx;
			.title-box{
				display: flex;
				align-items: center;
				justify-content: center;
				.status{
					font-size: 34upx;
					color: #000;
					font-weight: bold;
					line-height: 1;
				}
				.arrow{
					height: 24upx;
					margin-left: 20upx;
				}
			}
			.tip{
				font-size: 26upx;
				color: #8b8b8b;
				line-height: 1.6;
				margin-top: 20upx;
				text-align: center;
			}
			.btn-box{
				display: flex;
				align-items: center;
				justify-content: center;
				margin-top: 30upx;
				.btn{
					width: 184upx;
					height: 60upx;
					line-height: 60upx;
					border-radius: 30upx;
					text-align: center;
					font-size: 26upx;
					margin-right: 20upx;
					&:last-child{
						margin-right: 0;
					}
					&.buy{
						background-color: #03c821;
						color: #fff;
					}
					&.apply{
						background-color: #fff;
						color: #000;
						border: 2upx solid #dcdcdc;
					}
					&.contact{
						background-color: #fff;
						color: #000;
						margin-left: 0;
						border: 2upx solid #dcdcdc;
						&::after{
							display: none;
						}
					}
				}
			}
		}
		.pick-info{
			margin-top: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			.title{
				height: 80upx;
				line-height: 80upx;
				text-align: center;
				font-size: 24upx;
				color: #515151;
				border-bottom: 2upx solid #f2f2f2;
			}
			.inner{
				padding: 0 30upx;
				.time{
					height: 100upx;
					line-height: 100upx;
					font-size: 24upx;
					color: #585858;
					border-bottom: 2upx solid #f2f2f2;
				}
				.shop-address{
					padding: 30upx 0;
					.shop{
						line-height: 1.6;
						font-size: 24upx;
						color: #000;
						font-weight: bold;
					}
					.address{
						margin-top: 10upx;
						font-size: 24upx;
						color: #4e4e4e;
						line-height: 1.6;
					}
				}
			}
		}
		.goods-info{
			margin-top: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			overflow: hidden;
			padding: 0 30upx;
			.shop-name{
				height: 110upx;
				display: flex;
				align-items: center;
				border-bottom: 2upx solid #f2f2f2;
				.text{
					font-size: 30upx;
					color: #000;
				}
				.arrow{
					height: 24upx;
					margin-left: 20upx;
				}
			}
			.buy-goods-list{
				.inner{
					height: 300upx;
					overflow: hidden;
					transition: all .5s;
					&.show-all{
						height: auto;
					}
				}
				.item{
					padding: 20upx 0;
					display: flex;
					align-items: center;
					.img-box{
						width: 100upx;
						height: 104upx;
						border-radius: 8upx;
						background-color: #fafafa;
						margin-right: 20upx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.info-det{
						flex: 1;
						min-height: 104upx;
						display: flex;
						flex-direction: column;
						justify-content: space-between;
						.name-box{
							.tag{
								height: 32upx;
								border-radius: 4upx;
								background-color: #ff4c53;
								font-size: 20upx;
								color: #fff;
								padding: 0 10upx;
								margin-right: 10upx;
							}
							.name{
								font-size: 24upx;
								line-height: 32upx;
								color: #000;
							}
						}
						.num-price{
							display: flex;
							align-items: center;
							justify-content: space-between;
							.num{
								font-size: 24upx;
								color: #000;
							}
							.price{
								display: flex;
								align-items: center;
								.old{
									color: #979797;
									font-size: 22upx;
									margin-right: 10upx;
									text-decoration: line-through;
								}
								.new{
									color: #000;
									font-weight: bold;
									font-size: 22upx;
								}
							}
						}
					}
				}
				.show-more-goods{
					height: 56upx;
					line-height: 56upx;
					border-radius: 28upx;
					background-color: #f9f9f9;
					display: flex;
					align-items: center;
					justify-content: center;
					margin-bottom: 20upx;
					.text{
						font-size: 26upx;
						color: #757575;
					}
					.img{
						width: 26upx;
						margin-left: 14upx;
						transition: all .5s;
						&.show-all{
							transform: rotate(180deg);
						}
					}
				}
			}
			.fei-item{
				height: 80upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.left{
					display: flex;
					align-items: center;
					.label{
						font-size: 28upx;
						color: #000;
						line-height: 1;
					}
					.img{
						width: 32upx;
						height: 32upx;
						margin-left: 10upx;
					}
				}
				.price{
					font-size: 24upx;
					color: #000;
					font-weight: bold;
				}
				&.disc{
					.left{
						.tag{
							height: 32upx;
							line-height: 32upx;
							padding: 0 10upx;
							border-radius: 4upx;
							margin-right: 8upx;
							background-color: #ff4c48;
							font-size: 20upx;
							color: #fff;
						}
					}
					.price{
						color: #ff4c48;
					}
				}
			}
			.total-expens{
				height: 124upx;
				display: flex;
				align-items: center;
				justify-content: flex-end;
				border-top: 2upx solid #eeeeee;
				border-bottom: 2upx solid #eeeeee;
				.text{
					font-size: 26upx;
					color: #8e8e8e;
				}
				.num{
					font-size: 26upx;
					color: #f6585b;
				}
				.label{
					font-size: 26upx;
					color: #000;
					margin: 0 14upx;
				}
				.price{
					font-size: 36upx;
					color: #000;
					font-weight: bold;
				}
			}
			.call-merch{
				height: 110upx;
				display: flex;
				align-items: center;
				justify-content: center;
				.img{
					width: 36upx;
					height: 36upx;
					margin-right: 10upx;
				}
				.text{
					font-size: 28upx;
					color: #000;
				}
			}
		}
		.other-info{
			margin-top: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			overflow: hidden;
			padding: 0 30upx;
			.title{
				height: 100upx;
				line-height: 100upx;
				font-size: 30upx;
				color: #000;
				font-weight: bold;
				border-bottom: 2upx solid #eeeeee;
			}
			.item{
				height: 100upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				border-bottom: 2upx solid #eeeeee;
				&:last-child{
					border-bottom: none;
				}
				.left{
					display: flex;
					align-items: center;
					.label{
						font-size: 28upx;
						color: #000;
						font-weight: bold;
					}
					.text{
						font-size: 28upx;
						color: #1b1b1b;
					}
				}
				.copy-btn{
					width: 110upx;
					height: 48upx;
					border-radius: 24upx;
					line-height: 48upx;
					text-align: center;
					font-size: 28upx;
					color: #000;
					border: 2upx solid #d8d8d8;
				}
			}
		}
	}
</style>
