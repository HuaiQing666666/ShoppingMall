<template>
	<view class="content">
		<!-- 收货地址 -->
		<view class="receiv-address">
			<view class="address-box">
				<view class="left">
					<text class="tag">家</text>
					兰州市安昂却还是荆防败毒散
				</view>
				<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
			</view>
			<view class="user-name">
				<!-- <text class="text">张先生</text>
				<text class="text">185****7754</text> -->
				<text class="text">已有地址均不在配送范围</text>
			</view>
			<!-- 送达时间 -->
			<view class="time-service">
				<view class="time-box">
					<text class="label">送达时间</text>
					<view class="right">
						<text class="text">请选择时间</text>
						<image class="arrow" src="../../static/images/icon_arrow_r_b.png" mode="heightFix"></image>
					</view>
				</view>
				<view class="red-explain">无接触配送，可填写下方备注，如放门口或前台等位置</view>
			</view>
		</view>
		<!-- 商品等信息 -->
		<view class="goods-cont">
			<!-- 店铺名称 -->
			<view class="store-name">
				<view class="name">北京华联-飞天店</view>
				<view class="delivery">达达快送</view>
			</view>
			<!-- 商品列表 -->
			<view class="prod-list">
				<view v-for="(item,index) in 2" :key="index" class="item">
					<view class="img-box">
						<image src="../../static/logo.png" mode=""></image>
					</view>
					<view class="det-info">
						<view class="prod-name ellipsis">这里是商品名称这里是商品名称这里是商品</view>
						<view v-if="index == 0" class="speci">这里是规格等</view>
						<view class="price-box">
							<view class="left">
								<text class="text">￥15.8</text>
								<text class="text symbol">X</text>
								<text class="text">1</text>
							</view>
							<view class="price">￥15.8</view>
						</view>
					</view>
				</view>
				<!-- 商品总计 -->
				<view class="prod-total">
					共1件 / 1kg
				</view>
			</view>
			<!-- 其他费用 -->
			<view class="fei-item">
				<view class="left">
					<text class="label">运费</text>
					<image class="img" src="../../static/images/icon_info.png" mode=""></image>
				</view>
				<view class="price">￥1.2</view>
			</view>
			<view class="fei-item">
				<view class="left">
					<text class="label">包装服务</text>
					<image class="img" src="../../static/images/icon_info.png" mode=""></image>
				</view>
				<view class="price">￥1.2</view>
			</view>
			<view class="fei-item">
				<view class="left">
					<text class="label">红包</text>
				</view>
				<view class="des-text">暂无红包</view>
			</view>
			<!-- 实付金额 -->
			<view class="paid-amount">
				<view class="label">实付金额</view>
				<view class="num">￥21</view>
			</view>
		</view>
		<!-- 其他信息 -->
		<view class="info-cont">
			<view class="item">
				<view class="label">备注</view>
				<view class="right-box">
					<text class="tips">未填写</text>
					<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
				</view>
			</view>
			<view class="item">
				<view class="label">发票</view>
				<view class="right-box">
					<text class="tips">如需开票请联系商家</text>
				</view>
			</view>
			<view class="item">
				<view class="label">发票</view>
				<view class="right-box">
					<text class="text">缺货是电话与我沟通</text>
					<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
				</view>
			</view>
		</view>
		<!-- 底部按钮 -->
		<view class="bottom-box" :style="{paddingBottom: bottomBlackLineHeight +'rpx'}">
			<view class="inner">
				<text class="price">￥21</text>
				<view class="btn">提交订单</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				bottomBlackLineHeight: uni.getStorageSync('bottomBlackLineHeight'),
			}
		},
		onLoad() {
			// 设置顶部导航栏颜色
			uni.setNavigationBarColor({
			  frontColor: '#ffffff',
			  backgroundColor: '#43c851',
			  animation: {
				duration: 400,
				timingFunc: 'easeIn'
			  }
			})
		},
		methods: {
			
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
		min-height: 100%;
		position: relative;
		padding: 20upx;
		&::after{
			content: "";
			width: 100%;
			height: 240upx;
			background: linear-gradient(#43c851,transparent);
			position: absolute;
			top: 0;
			left: 0;
			z-index: -1;
		}
		.receiv-address{
			box-sizing: border-box;
			background-color: #fff;
			border-radius: 20upx;
			min-height: 270upx;
			padding: 30upx 30upx 0;
			.address-box{
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.left{
					max-width: 90%;
					font-size: 36upx;
					color: #000;
					font-weight: bold;
					display: flex;
					align-items: center;
					.tag{
						height: 26upx;
						line-height: 26upx;
						padding: 0 14upx;
						border-radius: 8upx;
						font-size: 20upx;
						color: #fff;
						margin-right: 10upx;
						background-color: #43c851;
					}
				}
				.arrow{
					height: 28upx;
				}
			}
			.user-name{
				display: flex;
				align-items: center;
				margin-top: 10upx;
				.text{
					font-size: 28upx;
					color: #434343;
					margin-right: 30upx;
				}
			}
			.time-service{
				border-top: 2upx solid #fcfcfc;
				padding: 20upx 0;
				margin-top: 20upx;
				.time-box{
					display: flex;
					align-items: center;
					justify-content: space-between;
					.label{
						font-size: 28upx;
						color: #000;
						font-weight: bold;
					}
					.right{
						display: flex;
						align-items: center;
						.text{
							font-size: 28upx;
							color: #4888c7;
							margin-right: 20upx;
						}
						.arrow{
							height: 24upx;
						}
					}
				}
				.red-explain{
					font-size: 22upx;
					color: #e25f63;
					margin-top: 20upx;
				}
			}
		}
		.goods-cont{
			margin-top: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			padding: 0 30upx;
			.store-name{
				padding: 30upx 0;
				display: flex;
				align-items: center;
				justify-content: space-between;
				border-bottom: 2upx solid #fcfcfc;
				.name{
					font-size: 28upx;
					color: #000;
					font-weight: bold;
				}
				.delivery{
					height: 30upx;
					line-height: 30upx;
					padding: 0 10upx;
					border-radius: 8upx;
					border: 2upx solid #99bfec;
					color: #0b6fe4;
					font-size: 20upx;
				}
			}
			.prod-list{
				margin-top: 20upx;
				.item{
					display: flex;
					margin-top: 20upx;
					.img-box{
						flex-shrink: 0;
						width: 90rpx;
						height: 90rpx;
						border-radius: 10rpx;
						overflow: hidden;
						background-color: #fafafa;
						margin-right: 20rpx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.det-info{
						min-height: 90upx;
						width: calc(100% - 110upx);
						.prod-name{
							font-size: 28upx;
							color: #000;
						}
						.speci{
							font-size: 24upx;
							color: #848484;
							margin-top: 10upx;
						}
						.price-box{
							margin-top: 20upx;
							display: flex;
							align-items: center;
							justify-content: space-between;
							.left{
								display: flex;
								align-items: center;
								.text{
									font-size: 20upx;
									color: #000;
									&.symbol{
										margin: 0 10upx;
									}
								}
							}
							.price{
								font-size: 22upx;
								color: #000;
								font-weight: bold;
							}
						}
					}
				}
				.prod-total{
					height: 50upx;
					line-height: 50upx;
					border-radius: 25upx;
					background-color: #f9f9f9;
					font-size: 26upx;
					text-align: center;
					color: #6d6d6d;
					margin-top: 30upx;
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
				.des-text{
					font-size: 24upx;
					color: #999999;
				}
			}
			.paid-amount{
				height: 100upx;
				display: flex;
				align-items: center;
				justify-content: flex-end;
				border-top: 2upx solid #e7e7e7;
				.label{
					font-size: 24upx;
					color: #000;
				}
				.num{
					font-size: 32upx;
					color: #000;
					font-weight: bold;
					margin-left: 20upx;
				}
			}
		}
		.info-cont{
			margin-top: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			margin-bottom: 150upx;
			.item{
				height: 100upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				border-bottom: 2upx solid #f8f8f8;
				padding: 0 30upx;
				&:last-child{
					border-bottom: none;
				}
				.label{
					font-size: 28upx;
					color: #000;
					font-weight: bold;
				}
				.right-box{
					display: flex;
					align-items: center;
					.tips{
						font-size: 26upx;
						color: #989898;
					}
					.text{
						font-size: 26upx;
						color: #000;
					}
					.arrow{
						height: 24upx;
						margin-left: 10upx;
					}
				}
			}
		}
		.bottom-box{
			box-sizing: border-box;
			width: 100%;
			position: fixed;
			padding: 0 20upx;
			left: 0;
			bottom: 0;
			background-color: #fff;
			border-top: 2upx solid #f6f6f6;
			.inner{
				height: 110upx;
				display: flex;
				align-items: center;
				justify-content: flex-end;
				.price{
					font-size: 26upx;
					font-weight: bold;
					color: #222222;
				}
				.btn{
					box-sizing: border-box;
					width: 200upx;
					height: 80upx;
					font-size: 26upx;
					color: #fff;
					line-height: 80upx;
					text-align: center;
					border-radius: 40upx;
					background: linear-gradient(to right,#01cb21,#01bd35);
					margin-left: 40upx;
				}
			}
		}
	}

</style>
