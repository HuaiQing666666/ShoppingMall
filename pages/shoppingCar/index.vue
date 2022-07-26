<template>
	<view class="content">
		<!-- 无数据 -->
		<view v-if="goodsList.length == 0" class="empty-goods">
			<image class="img" src="../../static/images/icon_shopcar.png" mode="widthFix"></image>
			<view class="title">购物车空空如也</view>
			<view class="btn" @click="goIndex">去首页看看</view>
		</view>
		<!-- 购物车列表 -->
		<view v-if="goodsList.length > 0" class="shopping-list">
			<!-- index==0：今天加入购物车的 -->
			<view v-for="(item,index) in goodsList" :key="index" class="item">
				<!-- 店铺信息 -->
				<view class="store-info">
					<view class="left">
						<label>
							<checkbox value="all" :checked="index ==0?false:true" />
						</label>
						<view class="info">
							<view class="top">
								<view class="text">北京华联飞天店</view>
								<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="heightFix"></image>
							</view>
							<view class="trans-info">
								<text class="text">47分钟 300m</text>
								<view class="line"></view>
								<text class="text">运费￥4</text>
							</view>
						</view>
					</view>
					<!-- 右上角：优惠券、清空购物车 -->
					<view class="empty-btn">
						<image src="../../static/images/icon_yhq.png" mode="heightFix"></image>
						<view class="line"></view>
						<view class="text">清空购物车</view>
					</view>
				</view>
				<!-- 是否勾选今日加购商品 -->
				<view class="has-chose-box">
					<!-- 否 -->
					<view v-if="index == 0" class="inner no-chose">仅勾选今日加购商品</view>
					<!-- 是 -->
					<view v-else class="inner">已勾选今日加购商品</view>
				</view>
				<!-- 物品列表 -->
				<view :class="index ==0?'car-goods-list today':'car-goods-list'">
					<view v-for="(goods,j) in 2" :key="j" class="goods-item">
						<label>
							<checkbox value="all" :checked="index ==0?false:true" />
						</label>
						<view class="img-box">
							<image src="../../static/logo.png" mode="aspectFill"></image>
						</view>
						<view class="det-info">
							<view class="title ellipsis">这里是商品名称这里是商品名称这里是商品名称这里是商品名称这里是商品名称</view>
							<view class="specifi">这里是商品规格</view>
							<!-- 价格加减 -->
							<view class="good-item-price">
								<view class="left-price">
									<view class="now">￥6.8</view>
									<view class="old">￥8.5</view>
								</view>
								<view class="number-box">
									<view class="btn" @click="subGoodsNum">－</view>
									<view class="input-box">
										<input type="text" v-model="value">
									</view>
									<view class="btn" @click="addGoodsNum">＋</view>
								</view>
							</view>
						</view>
					</view>
				</view>
				<!-- 店铺优惠：去凑单 -->
				<view v-if="index ==0" class="collect-orders">
					<text class="label">再买</text>
					<text class="num">22.2元</text>
					<text class="label">，用券最高可减</text>
					<text class="num">2元</text>
					<text class="num margin">去凑单</text>
					<image src="../../static/images/icon_arrow_r_r.png" mode="heightFix"></image>
				</view>
				<!-- 总价、按钮 -->
				<view class="item-bottom">
					<view class="total-price-box">
						<view class="label">总价</view>
						<view class="num-box">
							<view class="old">￥8.5</view>
							<view class="now">￥6.8</view>
						</view>
					</view>
					<view class="btn-box">
						<view class="btn buy">进店选购</view>
						<view :class="index ==0?'btn pay-no':'btn pay'">去结算</view>
					</view>
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
				goodsList: [1,2],
				value: 1,
			}
		},
		methods: {
			// 去首页
			goIndex() {
				uni.switchTab({
					url: '../index/index'
				})
			},
			// 商品数量减
			subGoodsNum() {
				const that = this
				this.value--
				if(this.value < 1) {
					uni.showModal({
						title: '提示',
						content: '确定删除该商品？',
						success: function (res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								that.value = 1
							}
						}
					})
				}
			},
			// 商品数量加
			addGoodsNum() {
				this.value++
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
		.empty-goods{
			background-color: #fff;
			border-radius: 20upx;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			padding: 30upx 0 20upx;
			margin-bottom: 20upx;
			.img{
				width: 140upx;
			}
			.title{
				font-size: 26upx;
				color: #333;
				margin-top: 30upx;
			}
			.btn{
				height: 52upx;
				line-height: 52upx;
				padding: 0 30upx;
				margin-top: 20upx;
				font-size: 24upx;
				color: #fff;
				border-radius: 26upx;
				background: linear-gradient(to right,#01ce39,#44dc6f);
			}
		}
		.shopping-list{
			.item{
				background-color: #fff;
				border-radius: 10upx;
				overflow: hidden;
				margin-bottom: 16upx;
				.store-info{
					background-color: #fdfdfd;
					display: flex;
					justify-content: space-between;
					padding: 20upx;
					.left{
						display: flex;
						align-items: center;
						label{
							padding-bottom: 6upx;
						}
						.info{
							margin-left: 16upx;
							.top{
								display: flex;
								align-items: center;
								.text{
									font-size: 26upx;
									color: #000;
									margin-right: 6upx;
								}
								.arrow{
									flex-shrink: 0;
									height: 24upx;
								}
							}
							.trans-info{
								display: flex;
								align-items: center;
								margin-top: 6upx;
								.text{
									font-size: 24upx;
									color: #464646;
								}
								.line{
									width: 1px;
									height: 20upx;
									margin: 0 12upx;
									background-color: #bfbfbf;
								}
							}
						}
					}
					.empty-btn{
						flex-shrink: 0;
						align-self: flex-start;
						display: flex;
						align-items: center;
						image{
							height: 36upx;
						}
						.line{
							width: 2upx;
							height: 18upx;
							background-color: #a3a0a1;
							margin: 0 8upx;
						}
						.text{
							font-size: 20upx;
							color: #a3a0a1;
						}
					}
				}
				.has-chose-box{
					padding: 20upx;
					background-color: #fff;
					.inner{
						height: 46upx;
						line-height: 46upx;
						text-align: center;
						font-size: 24upx;
						color: #939393;
						background-color: #f6f6f6;
						border-radius: 23upx;
						&.no-chose{
							color: #df3e3e;
							background-color: #fef3f1;	
						}
					}
				}
				.car-goods-list{
					background-color: #fff;
					&.today{
						background-color: #fef3f1;
					}
					.goods-item{
						display: flex;
						align-items: center;
						padding: 20upx;
						.img-box{
							flex-shrink: 0;
							width: 90upx;
							height: 90upx;
							border-radius: 10upx;
							overflow: hidden;
							background-color: #fff;
							margin-left: 20upx;
							margin-right: 20upx;
							image{
								width: 100%;
								height: 100%;
							}
						}
						.det-info{
							flex: 1;
							max-width: 75%;
							.title{
								max-width: 85%;
								font-size: 24upx;
								color: #000;
							}
							.specifi{
								font-size: 20upx;
								color: #8a8a8a;
								margin-top: 10upx;
							}
							.good-item-price{
								display: flex;
								align-items: center;
								justify-content: space-between;
								margin-top: 20upx;
								.left-price{
									display: flex;
									align-items: center;
									.now{
										font-size: 24upx;
										color: #df3e3e;
										font-weight: bold;
									}
									.old{
										text-decoration: line-through;
										font-size: 24upx;
										color: #949091;
										margin-left: 10upx;
									}
								}
								.number-box{
									display: flex;
									align-items: center;
									height: 40upx;
									border: 2upx solid #f1f1f1;
									border-radius: 20upx;
									.btn{
										width: 40upx;
										text-align: center;
										line-height: 40upx;
										color: #1c1c1c;
										font-size: 24upx;
									}
									.input-box{
										width: 66upx;
										display: flex;
										align-items: center;
										justify-content: center;
										border-left: 2upx solid #f1f1f1;
										border-right: 2upx solid #f1f1f1;
										padding: 0 6upx;
										input{
											font-size: 24upx;
											color: #000;
											text-align: center;
										}
									}
								}
							}
						}
					}
				}
				.collect-orders{
					height: 50upx;
					background-color: #fff6cd;
					display: flex;
					align-items: center;
					justify-content: center;
					.label{
						font-size: 22upx;
						color: #5a2800;
					}
					.num{
						font-size: 22upx;
						color: #ce6562;
						&.margin{
							margin-left: 20upx;
						}
					}
					image{
						height: 20upx;
					}
				}
				.item-bottom{
					padding: 0 20upx;
					.total-price-box{
						height: 70upx;
						border-top: 2upx solid #fafafa;
						border-bottom: 2upx solid #fafafa;
						display: flex;
						align-items: center;
						justify-content: space-between;
						.label{
							font-size: 28upx;
							color: #000;
						}
						.num-box{
							display: flex;
							align-items: center;
							.now{
								font-size: 24upx;
								color: #000;
								font-weight: bold;
							}
							.old{
								text-decoration: line-through;
								font-size: 24upx;
								color: #979797;
								margin-right: 10upx;
							}
						}
					}
					.btn-box{
						padding: 20upx 0;
						display: flex;
						align-items: center;
						justify-content: flex-end;
						.btn{
							width: 190upx;
							height: 70upx;
							line-height: 70upx;
							text-align: center;
							font-size: 24upx;
							border-radius: 35upx;
							margin-left: 8upx;
							&.buy{
								background-color: #e5f9ed;
								color: #35d861;
							}
							&.pay{
								background-color: #35d861;
								color: #ffffff;
							}
							&.pay-no{
								background-color: #999999;
								color: #ffffff;
							}
						}
					}
				}
			}
		}
	}
</style>
