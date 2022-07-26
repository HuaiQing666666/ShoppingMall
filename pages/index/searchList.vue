<template>
	<view class="content" :style="{paddingTop: topCountHeight +'px'}">
		<view class="top-cont" id="topCount" :style="{paddingTop: statusBarHeight +'px'}">
			<view class="inner">
				<image class="back" src="../../static/images/icon_back_b.png" mode="heightFix" @click="back"></image>
				<view class="screen-box">
					<image class="search" src="../../static/images/icon_search.png" mode=""></image>
					<view class="search-text ellipsis">上一个页面带过来的搜索文字</view>
				</view>
			</view>
			<!-- 商家列表 -->
			<view class="business-box">
				<view class="scroll-box">
					<scroll-view class="scroll-inner" scroll-x="true" >
						<view class="busi-list">
							<view class="item all active">
								<image class="img" src="../../static/images/icon_applicat.png" mode=""></image>
								<text class="text">全部</text>
							</view>
							<view v-for="(item,index) in 5" :key="index" class="item">
								<view class="img-box">
									<image src="../../static/logo.png" mode=""></image>
								</view>
								<view class="info-box">
									<view class="title ellipsis">这里是商家名称名称名称名称</view>
									<view v-if="index == 0" class="tag">免运费</view>
									<view v-else class="tag coupon">已领10元券</view>
								</view>
							</view>
						</view>
					</scroll-view>
				</view>
				<view class="arrow-box" @click="openBusiPop">
					<image class="arrow" src="../../static/images/icon_arrow_b_d.png" mode="widthFix"></image>
				</view>
			</view>
			<!-- 排序 -->
			<view class="sort-box">
				<view :class="isCompSort?'item comp active':'item comp'" @click="sortChose()">
					<text class="text">综合排序</text>
					<image class="arrow gray" src="../../static/images/icon_arrow_b_d.png" mode=""></image>
					<image class="arrow green" src="../../static/images/icon_arrow_b_g.png" mode=""></image>
				</view>
				<!-- 综合排序下拉选择 -->
				<view :class="compSelectShow?'comp-select-box show':'comp-select-box'">
					<view class="item active">
						<text class="text">综合排序</text>
						<image class="img" src="../../static/images/icon_pair.png" mode=""></image>
					</view>
					<view class="item">
						<text class="text">优惠</text>
						<image class="img" src="../../static/images/icon_pair.png" mode=""></image>
					</view>
					<view class="item">
						<text class="text">销量</text>
						<image class="img" src="../../static/images/icon_pair.png" mode=""></image>
					</view>
					<view class="item">
						<text class="text">距离</text>
						<image class="img" src="../../static/images/icon_pair.png" mode=""></image>
					</view>
				</view>
				<view class="item">
					<text class="text">速度</text>
				</view>
				<view :class="sortPriceChose?'item active':'item'" @click="shotPrice">
					<text class="text">价格</text>
					<view v-if="!sortPriceChose" class="triangle-box">
						<image class="triangle" src="../../static/images/triangle_up.png" mode=""></image>
						<image class="triangle" src="../../static/images/triangle_down.png" mode=""></image>
					</view>
					<view v-if="sortPriceChose && sortPrice == 1" class="triangle-box">
						<image class="triangle" src="../../static/images/triangle_up_g.png" mode=""></image>
						<image class="triangle" src="../../static/images/triangle_down.png" mode=""></image>
					</view>
					<view v-if="sortPriceChose && sortPrice == 2" class="triangle-box">
						<image class="triangle" src="../../static/images/triangle_up.png" mode=""></image>
						<image class="triangle" src="../../static/images/triangle_down_g.png" mode=""></image>
					</view>
				</view>
				<view class="item" @click="openFilter">
					<text class="text">筛选</text>
					<image class="screen" src="../../static/images/icon_screen.png" mode=""></image>
				</view>
			</view>
			
		</view>
		<!-- 下拉蒙版 -->
		<view :class="maskShow?'my-mask show':'my-mask'"></view>
		<!-- 更多商家下拉 -->
		<u-popup :show="showMoreBusi" mode="top" :round="20" @close="closeBusiPop" @open="openBusiPop">
			<view class="busi-dialog" :style="{paddingTop: statusBarHeight +'px'}">
				<view class="title-box">
					<view class="label">5个商家有结果</view>
					<image class="arrow" src="../../static/images/icon_arrow_b_d.png" mode="widthFix" @click="closeBusiPop"></image>
				</view>
				<view class="busi-list">
					<view class="item all active">
						<image class="img" src="../../static/images/icon_app_b.png" mode=""></image>
						<text class="text">全部</text>
					</view>
					<view v-for="(item,index) in 5" :key="index" class="item">
						<view class="img-box">
							<image src="../../static/logo.png" mode=""></image>
						</view>
						<view class="info-box">
							<view class="title ellipsis">这里是商家名称名称名称名称</view>
							<view class="tag-box">
								<view class="tag">免运费</view>
								<view class="tag coupon">已领10元券</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</u-popup>
		<!-- 筛选框 -->
		<u-popup :show="filterContShow" mode="right" @close="closeFilter" @open="openFilter">
			<view class="filetr-dialog" :style="{paddingTop: statusBarHeight +'px'}">
				<view class="inner">
					<view class="filter-item">
						<view class="title-box">
							<view class="label">分类</view>
						</view>
						<view class="cate-list">
							<view v-for="(item,index) in 3" :key="index" :class="index == 0?'item active':'item'">分类名称</view>
						</view>
					</view>
					<view class="filter-item">
						<view class="title-box">
							<view class="label">价格区间</view>
						</view>
						<view class="price-range">
							<view class="input-box">
								<input type="number" placeholder="最低价" placeholder-style="font-size:22upx;color:#c7c7c7;">
							</view>
							<view class="symbol">-</view>
							<view class="input-box">
								<input type="number" placeholder="最低价" placeholder-style="font-size:22upx;color:#c7c7c7;">
							</view>
						</view>
					</view>
					<view class="filter-item">
						<view class="title-box">
							<view class="label">品牌</view>
						</view>
						<view class="cate-list">
							<view v-for="(item,index) in 4" :key="index" :class="index == 0?'item active':'item'">分类名称</view>
						</view>
					</view>
					<view class="filter-item">
						<view class="title-box">
							<view class="label">规格</view>
						</view>
						<view class="cate-list">
							<view v-for="(item,index) in 4" :key="index" :class="index == 0?'item active':'item'">分类名称</view>
						</view>
					</view>
				</view>
				<view class="btn-box">
					<view class="btn">重置</view>
					<view class="btn submit">查看</view>
				</view>
			</view>
		</u-popup>
		<!-- 商品列表 -->
		<view class="goods-cont">
			<scroll-view :scroll-y="true" >
				<view v-for="(goods,index) in 3" :key="index" class="goods-item">
					<!-- 商品信息 -->
					<view class="info-box">
						<view class="img-box">
							<image class="img" src="../../static/logo.png" mode="aspectFill"></image>
						</view>
						<view class="inner">
							<view class="title ellipsis2">这里是商品名称这里是商品名称这里是商品名称这里是商品名称这里是商品名称这里是商品名称这里是商品名称</view>
							<view class="sub-title ellipsis">这里是其他说明文字这里是其他说明文字这里是其他说明文字这里是其他说明文字z</view>
							<view class="price-box">
								<view class="price">
									<text class="num">￥218</text>
									<text class="unit">起</text>
								</view>
								<view class="old-price">￥399</view>
								<view class="sale-num">月售 0</view>
							</view>
							<view class="discount">
								<view class="offer-item">秒杀5.47折限5份</view>
								<view class="coup-item">满99减30</view>
							</view>
							<view v-if="index == 0" class="remarks ellipsis">【赠品】餐具、数字蜡烛、生日帽、代写生日贺卡等等等等等</view>
						</view>
					</view>
					<!-- 商家信息 -->
					<view class="busi-info">
						<view class="img-box">
							<image class="img" src="../../static/logo.png" mode="aspectFill"></image>
						</view>
						<view class="info-inner">
							<view class="title-box">
								<view class="title ellipsis">这里是店名称</view>
								<image class="arrow" src="../../static/images/icon_arrow_r.png" mode="aspectFill"></image>
							</view>
							<view class="delivery-info">
								<view v-if="index == 0" class="free">免运费</view>
								<view v-else class="fee">运费￥4.5</view>
								<view class="right">
									<text class="text">60分钟</text>
									<text class="line"></text>
									<text class="text">19.7km</text>
								</view>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				statusBarHeight: uni.getStorageSync('statusBarHeight'),
				showMoreBusi: false,
				isCompSort: true, // 综合排序是否选中
				topCountHeight: 0, // 顶部固定元素高度
				compSelectShow: false, // 综合排序下拉展开
				maskShow: false, // 自定义蒙版
				sortPriceChose: false, // 价格排序是否选中
				sortPrice: 2, // 价格排序: 1 升序，2降序
				filterContShow: false, // 筛选框
			}
		},
		onLoad() {
			const query = uni.createSelectorQuery().in(this);
			query.select('#topCount').boundingClientRect(data => {
				this.topCountHeight = data.height
				console.log(this.topCountHeight)
			}).exec();
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			// 打开更多商家弹框
			openBusiPop() {
				this.showMoreBusi = true
			},
			// 关闭更多商家弹框
			closeBusiPop() {
				this.showMoreBusi = false
			},
			// 排序选择
			sortChose() {
				this.compSelectShow = !this.compSelectShow
				this.maskShow = !this.maskShow
			},
			// 价格排序
			shotPrice() {
				this.sortPriceChose = true
				if(this.sortPrice == 1) {
					this.sortPrice = 2
				} else if(this.sortPrice == 2) {
					this.sortPrice = 1
				}
			},
			// 打开筛选框
			openFilter() {
				this.filterContShow = true
			},
			// 关闭筛选框
			closeFilter() {
				this.filterContShow = false
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
		background-color: #f6f6f6;
	}
</style>
<style scoped lang="scss">
	.my-mask{
		width: 100%;
		height: 100%;
		position: fixed;
		top: 0;
		left: 0;
		background-color: rgba(0,0,0,0.6);
		z-index: 888;
		display: none;
		&.show{
			display: block;
		}
	}
	.content{
		height: 100%;
		.top-cont{
			width: 100%;
			background-color: #f6f6f6;
			position: fixed;
			top: 0;
			left: 0;
			z-index: 999;
			.inner{
				height: 88upx;
				display: flex;
				align-items: center;
				padding-right: 240upx;
				padding-left: 30upx;
				.back{
					width: 34upx;
					height: 34upx;
					margin-right: 24upx;
				}
				.screen-box{
					flex: 1;
					height: 60upx;
					border-radius: 30upx;
					background-color: #fff;
					display: flex;
					align-items: center;
					padding: 0 20upx;
					.search{
						width: 30upx;
						height: 30upx;
						margin-right: 20upx;
					}
					.search-text{
						max-width: 250upx;
						height: 40upx;
						font-size: 22upx;
						color: #343434;
						line-height: 40upx;
						padding: 0 20upx;
						border-radius: 20upx;
						background-color: #f6f6f6;
					}
				}
			}
			.business-box{
				display: flex;
				align-items: center;
				padding-left: 20upx;
				.scroll-box{
					width: calc(100% - 70upx);
					.scroll-inner{
						padding-right: 20upx;
					}
					.busi-list{
						display: flex;
						align-items: center;
						padding-bottom: 10upx;
						.item{
							flex-shrink: 0;
							height: 90upx;
							width: 290upx;
							margin-right: 12upx;
							background-color: #fff;
							border-radius: 10upx;
							display: flex;
							align-items: center;
							padding: 14upx 16upx;
							.img-box{
								width: 65upx;
								height: 65upx;
								border-radius: 10upx;
								overflow: hidden;
								margin-right: 10upx;
								image{
									width: 100%;
									height: 100%;
								}
							}
							.info-box{
								width: calc(100% - 75upx);
								height: 65upx;
								display: flex;
								flex-direction: column;
								align-items: flex-start;
								justify-content: space-between;
								.title{
									width: 100%;
									font-size: 22upx;
									color: #000;
									line-height: 1;
								}
								.tag{
									height: 30upx;
									line-height: 24upx;
									padding: 0 10upx;
									border-radius: 8upx;
									border: 2upx solid #9bc8ec;
									font-size: 18upx;
									color: #006cd5;
									background-color: #fbffff;
									margin-right: 8upx;
									&.coupon{
										color: #e05363;
										border-color: #f0ccd3;
										background-color: #fff7f4;
									}
								}
							}
							&.all{
								justify-content: center;
								width: 130upx;
								.img{
									width: 30upx;
									height: 30upx;
									margin-right: 6upx;
								}
								.text{
									font-size: 26upx;
									color: #fff;
								}
							}
							&.active{
								background-color: #31d65e;
								position: relative;
								&::after{
									content: "";
									width: 0;
									height: 0;
									border-left: 10upx solid transparent;
									border-right: 10upx solid transparent;
									border-top: 10upx solid #31d65e;
									position: absolute;
									left: 50%;
									transform: translateX(-50%);
									bottom: -10upx;
									z-index: 99;
								}
							}
						}
					}
				}
				.arrow-box{
					width: 70upx;
					height: 90upx;
					display: flex;
					align-items: center;
					justify-content: center;
					margin-bottom: 10upx;
					box-shadow: -10upx 0px 20upx -14upx rgba(0,0,0,0.36);
					z-index: 10;
					.arrow{
						width: 30upx;
						height: 30upx;
					}
				}
			}
			.sort-box{
				height: 80upx;
				padding: 0 50upx 0 30upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				position: relative;
				.item{
					display: flex;
					align-items: center;
					&.comp{
						.gray{
							display: block;
						}
						.green{
							display: none;
						}
						&.active{
							.gray{
								display: none;
							}
							.green{
								display: block;
							}
						}
					}
					&.active{
						.text{
							color: #31d65e;
						}
					}
					.text{
						font-size: 24upx;
						color: #242424;
						line-height: 1;
					}
					.arrow{
						width: 22upx;
						height: 22upx;
						margin-left: 10upx;
						margin-top: 5rpx;
					}
					.triangle-box{
						display: flex;
						flex-direction: column;
						margin-left: 10upx;
						margin-top: 4upx;
						.triangle{
							width: 14upx;
							height: 14upx;
						}
					}
					.screen{
						margin-left: 10upx;
						width: 20upx;
						height: 20upx;
					}
				}
				.comp-select-box{
					width: 100%;
					background-color: #ffff;
					position: absolute;
					left: 0;
					top: 80upx;
					border-radius: 0 0 20upx 20upx;
					padding: 0 30upx;
					display: none;
					&.show{
						display: block;
					}
					.item{
						height: 80upx;
						display: flex;
						align-items: center;
						justify-content: space-between;
						border-bottom: 2upx solid #ededed;
						.text{
							font-size: 26upx;
							color: #333;
						}
						.img{
							width: 30upx;
							height: 30upx;
							display: none;
						}
						&.active{
							.text{
								color: #31d65e;
							}
							.img{
								display: block;
							}
						}
					}
				}
			}
		}
		.busi-dialog{
			.title-box{
				margin-top: 88upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				padding: 0 35upx 30upx;
				.label{
					font-size: 26upx;
					color: #000;
				}
				.arrow{
					width: 30upx;
					transform: rotate(-180deg);
				}
			}
			.busi-list{
				display: flex;
				flex-wrap: wrap;
				padding-bottom: 10upx;
				padding: 0 20upx;
				.item{
					flex-shrink: 0;
					height: 100upx;
					width: calc(50% - 12upx);
					margin-right: 20upx;
					background-color: #fff;
					border-radius: 10upx;
					display: flex;
					align-items: center;
					padding: 16upx;
					margin-bottom: 20upx;
					background-color: #f8f8f8;
					&:nth-child(2n) {
						margin-right: 0;
					}
					.img-box{
						width: 68upx;
						height: 68upx;
						border-radius: 10upx;
						overflow: hidden;
						margin-right: 10upx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.info-box{
						width: calc(100% - 78upx);
						height: 68upx;
						display: flex;
						flex-direction: column;
						align-items: flex-start;
						justify-content: space-between;
						.title{
							width: 100%;
							font-size: 22upx;
							color: #000;
							line-height: 1;
						}
						.tag-box{
							display: flex;
							align-items: center;
						}
						.tag{
							height: 30upx;
							line-height: 24upx;
							padding: 0 10upx;
							border-radius: 8upx;
							border: 2upx solid #9bc8ec;
							font-size: 18upx;
							color: #006cd5;
							background-color: #fbffff;
							margin-right: 8upx;
							&.coupon{
								color: #e05363;
								border-color: #f0ccd3;
								background-color: #fff7f4;
							}
						}
					}
					&.all{
						justify-content: center;
						.img{
							width: 30upx;
							height: 30upx;
							margin-right: 6upx;
						}
						.text{
							font-size: 26upx;
							color: #000;
						}
					}
					&.active{
						background-color: #e4fbe9;
					}
				}
			}
		}
		.goods-cont{
			padding: 0 22upx;
			.goods-item{
				background-color: #fff;
				border-radius: 20upx;
				margin-bottom: 10upx;
				padding: 0 20upx;
				.info-box{
					display: flex;
					padding: 20upx 0;
					border-bottom: 2upx solid #ededed;
					.img-box{
						width: 176upx;
						height: 176upx;
						border-radius: 10upx;
						overflow: hidden;
						margin-right: 14upx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.inner{
						width: calc(100% - 190upx);
						min-height: 176upx;
						display: flex;
						flex-direction: column;
						padding-top: 8upx;
						// justify-content: space-between;
						.title{
							font-size: 24upx;
							color: #131313;
							font-weight: bold;
						}
						.sub-title{
							font-size: 22upx;
							color: #926c39;
							margin-top: 12upx;
							line-height: 1;
						}
						.price-box{
							display: flex;
							align-items: center;
							margin-top: 20upx;
							.price{
								display: flex;
								.num{
									font-size: 26upx;
									color: #f11512;
									font-weight: bold;
									line-height: 1;
								}
								.unit{
									font-size: 20upx;
									color: #f11512;
									line-height: 1.3;
									align-self: flex-end;
								}
							}
							.old-price{
								margin-left: 8upx;
								font-size: 20upx;
								color: #a4a4a4;
								text-decoration: line-through;
							}
							.sale-num{
								font-size: 22upx;
								color: #5e5e5e;
								margin-left: 16upx;
							}
						}
						.discount{
							display: flex;
							align-items: center;
							margin-top: 15upx;
							.offer-item{
								box-sizing: border-box;
								flex-shrink: 0;
								height: 32upx;
								line-height: 32upx;
								display: flex;
								align-items: center;
								padding: 0 10upx;
								border: 2upx solid #ee93a5;
								border-radius: 10upx;
								font-size: 18upx;
								color: #bc1428;
								margin-right: 8upx;
								margin-bottom: 8upx;
							}
							.coup-item{
								height: 32upx;
								line-height: 26upx;
								border: 2upx solid #e7d2d0;
								padding: 0 14upx;
								font-size: 18upx;
								color: #da1b1e;
								border-radius: 8upx;
								position: relative;
								margin-right: 8upx;
								margin-bottom: 8upx;
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
									right: -14upx;
									top: 16%;
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
						.remarks{
							font-size: 20upx;
							margin-top: 12upx;
							color: #959597;
						}
					}
				}
				.busi-info{
					padding: 20upx 0;
					display: flex;
					align-items: center;
					.img-box{
						width: 55upx;
						height: 55upx;
						border-radius: 8upx;
						overflow: hidden;
						margin-right: 15upx;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.info-inner{
						width: calc(100% - 70upx);
						height: 55upx;
						display: flex;
						flex-direction: column;
						justify-content: space-between;
						.title-box{
							width: 100%;
							display: flex;
							align-items: center;
							.title{
								max-width: 90%;
								font-size: 20upx;
								color: #000;
								font-weight: bold;
								margin-right: 6upx;
							}
							.arrow{
								width: 18upx;
								height: 18upx;
							}
						}
						.delivery-info{
							display: flex;
							align-items: center;
							justify-content: space-between;
							.free{
								font-size: 22upx;
								color: #ec1c1d;
								font-weight: bold;
								line-height: 1;
							}
							.fee{
								font-size: 22upx;
								color: #474747;
								line-height: 1;
							}
							.right{
								display: flex;
								align-items: center;
								.text{
									font-size: 20upx;
									color: #474747;
									line-height: 1;
								}
								.line{
									width: 2upx;
									height: 15upx;
									background-color: #dcdcdc;
									margin: 0 10upx;
								}
							}
						}
					}
				}
			}
		}
		
	}
	.filetr-dialog{
		width: 600upx;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		.inner{
			flex: 1;
			padding: 70upx 30upx 0;
			.filter-item{
				border-bottom: 2upx solid #f7f7f7;
				&:last-child{
					border-bottom: none;
				}
				.title-box{
					display: flex;
					align-items: center;
					justify-content: space-between;
					padding: 20upx 0;
					.label{
						font-size: 26upx;
						color: #333;
					}
					.arrow{
						width: 30upx;
						height: 30upx;
					}
				}
				.cate-list{
					display: flex;
					flex-wrap: wrap;
					.item{
						width: 32%;
						height: 55upx;
						line-height: 55upx;
						text-align: center;
						font-size: 22upx;
						color: #000;
						margin-right: 2%;
						margin-bottom: 20upx;
						background-color: #f8f8f8;
						border-radius: 8upx;
						&:nth-child(3n) {
							margin-right: 0;
						}
						&.active{
							background-color: rgba(49, 214, 94, 0.1);
							color: #31d65e;
						}
					}
				}
				.price-range{
					display: flex;
					align-items: center;
					justify-content: space-between;
					margin-bottom: 20upx;
					.input-box{
						width: 248upx;
						height: 60upx;
						display: flex;
						align-items: center;
						justify-content: center;
						background-color: #f8f8f8;
						border-radius: 8upx;
						input{
							text-align: center;
							font-size: 26upx;
							color: #333;
						}
					}
					.symbol{
						font-size: 28upx;
						color: #000;
						font-weight: bold;
					}
				}
			}
		}
		.btn-box{
			display: flex;
			align-items: center;
			.btn{
				width: 50%;
				height: 85upx;
				line-height: 85upx;
				text-align: center;
				font-size: 24upx;
				color: #c4c4c4;
				&.submit{
					color: #fff;
					background-color: #02cc22;
				}
			}
		}
	}
</style>
