<template>
	<view class="content" :style="{paddingTop: topCountHeight +'px'}">
		<view class="top-cont" id="topCount">
			<!-- 排序 -->
			<view class="sort-box">
				<view class="left">
					<text :class="sortMode == 1?'text active':'text'" @click="choseSort(1)">综合排序</text>
					<text :class="sortMode == 2?'text active':'text'" @click="choseSort(2)">销量</text>
					<text :class="sortMode == 3?'text active':'text'" @click="choseSort(3)">距离</text>
				</view>
				<view class="right" @click="openFilter">
					<text class="text">筛选</text>
					<image class="screen" src="../../static/images/icon_screen.png" mode=""></image>
				</view>
			</view>
		</view>
		<!-- 筛选框 -->
		<u-popup :show="filterContShow" :safeAreaInsetBottom="false" mode="top" @close="closeFilter" @open="openFilter">
			<view class="filetr-dialog">
				<view class="inner">
					<view class="filter-item">
						<view class="title-box">
							<view class="label">商家特色</view>
						</view>
						<view class="cate-list">
							<view v-for="(item,index) in 3" :key="index" :class="index == 0?'item active':'item'">分类名称</view>
						</view>
					</view>
					<view class="filter-item">
						<view class="title-box">
							<view class="label">优惠活动</view>
						</view>
						<view class="cate-list">
							<view v-for="(item,index) in 4" :key="index" :class="index == 0?'item active':'item'">分类名称</view>
						</view>
					</view>
					<view class="filter-item">
						<view class="title-box">
							<view class="label">门店类型</view>
						</view>
						<view class="cate-list">
							<view v-for="(item,index) in 4" :key="index" :class="index == 0?'item active':'item'">分类名称</view>
						</view>
					</view>
				</view>
				<view class="btn-box">
					<view class="btn">重置</view>
					<view class="btn submit">查看86个店铺</view>
				</view>
			</view>
		</u-popup>
		<!-- 商家列表 --> 
		<view class="busi-list" :style="{paddingBottom: bottomBlackLineHeight +'rpx'}">
			<view v-for="(item,index) in busiList" :key="index" class="item">
				<view class="img-box">
					<image class="img" src="../../static/logo.png" mode="aspectFill"></image>
					<!-- 角标 -->
					<u-badge max="99" :value="1"></u-badge>
				</view>
				<view class="info-cont">
					<view class="info-inner">
						<view class="busi-name ellipsis">这里是商铺名称</view>
						<view class="sale-info">
							<view class="left">
								<u-rate :count="5" v-model="4.8" active-color="#fba929" inactive-color="#b2b2b2" readonly></u-rate>
								<text class="score">4.8</text>
								<text class="sale">月售百+</text>
							</view>
							<view class="right">
								<text class="text">60分钟</text>
								<text class="line"></text>
								<text class="text">222m</text>
							</view>
						</view>
						<!-- 配送信息 -->
						<view class="deliv-info">
							<view class="left">
								<text class="text">起送￥0</text>
								<text class="line"></text>
								<text class="text">免运费</text>
							</view>
							<view class="mode">达达快送</view>
						</view>
					</view>
					<!-- 优惠券 -->
					<view class="coupons">
						<view class="item">已领10元券</view>
					</view>
					<!-- 附近商家 -->
					<view class="nearby-busi">
						<view class="title-box" @click="showNebBusi(index)">
							<view class="left">
								<image src="../../static/images/icon_busi.png" mode="aspectFill"></image>
								<text class="text">附件还有5家</text>
							</view>
							<image :class="item.nearbyBusiShow?'arrow show':'arrow'" src="../../static/images/icon_arrow_b_d.png" mode="aspectFill"></image>
						</view>
						<view :class="item.nearbyBusiShow?'neb-busi-list show':'neb-busi-list'">
							<view v-for="(busi,j) in 3" :key="j" class="busi-item">
								<view class="name">店铺-安宁大学城店</view>
								<view class="distance">1.6km</view>
							</view>
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
				statusBarHeight: uni.getStorageSync('statusBarHeight'),
				bottomBlackLineHeight: uni.getStorageSync('bottomBlackLineHeight'),
				topCountHeight: 0, // 顶部固定元素高度
				sortMode: 1, // 选中的排序方式
				filterContShow: false, // 筛选框
				busiList:[
					{
						name: '商铺1',
						nearbyBusiShow: false, // 控制是否限时其他商家
					},
					{
						name: '商铺1',
						nearbyBusiShow: false,
					},
					{
						name: '商铺1',
						nearbyBusiShow: false,
					},
					{
						name: '商铺1',
						nearbyBusiShow: false,
					},
					{
						name: '商铺1',
						nearbyBusiShow: false,
					}
				]
			}
		},
		onLoad() {
			const query = uni.createSelectorQuery().in(this);
			query.select('#topCount').boundingClientRect(data => {
				this.topCountHeight = data.height
			}).exec();
		},
		methods: {
			// 排序选择
			choseSort(index) {
				this.sortMode = index
			},
			// 打开筛选框
			openFilter() {
				this.filterContShow = true
			},
			// 关闭筛选框
			closeFilter() {
				this.filterContShow = false
			},
			// 站开合并附近其他商家
			showNebBusi(index) {
				this.busiList[index].nearbyBusiShow = !this.busiList[index].nearbyBusiShow
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
		background-color: #ffffff;
	}
</style>
<style scoped lang="scss">
	.content{
		min-height: 100%;
		.top-cont{
			width: 100%;
			position: fixed;
			top: 0;
			left: 0;
			background-color: #fff;
			z-index: 999;
			.sort-box{
				height: 80upx;
				padding: 0 50upx 0 30upx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.left{
					display: flex;
					align-items: center;
					.text{
						font-size: 22upx;
						color: #121212;
						margin-right: 50upx;
						&:last-child{
							margin-right: 0;
						}
						&.active{
							color: #31d65e;
						}
					}
				}
				.right{
					display: flex;
					align-items: center;
					.text{
						font-size: 24upx;
						color: #242424;
						line-height: 1;
					}
					.screen{
						margin-left: 10upx;
						width: 20upx;
						height: 20upx;
					}
				}
			}
		}
		.busi-list{
			.item{
				padding: 20upx 0 0 20upx;
				margin-bottom: 20upx;
				display: flex;
				&:last-child{
					.info-cont{
						border-bottom: none;
					}
				}
				.img-box{
					width: 110upx;
					height: 110upx;
					margin-right: 20upx;
					position: relative;
					image{
						width: 100%;
						height: 100%;
						border-radius: 8upx;
					}
					/deep/.u-badge{
						position: absolute;
						top: -12upx;
						right: -12upx;
						z-index: 99;
					}
				}
				.info-cont{
					width: calc(100% - 130upx);
					padding-bottom: 20upx;
					padding-right: 20upx;
					border-bottom: 2upx solid #f7f7f7;
					.info-inner{
						width: 100%;
						height: 110upx;
						display: flex;
						flex-direction: column;
						justify-content: space-between;
						.busi-name{
							width: 100%;
							font-size: 28upx;
							color: #000;
							font-weight: bold;
						}
						.sale-info{
							display: flex;
							align-items: center;
							justify-content: space-between;
							.left{
								display: flex;
								align-items: center;
								.score{
									font-size: 22upx;
									color: #fba929;
								}
								.sale{
									font-size: 22upx;
									color: #525252;
									margin-left: 12upx;
								}
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
						.deliv-info{
							display: flex;
							align-items: center;
							justify-content: space-between;
							.left{
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
							.mode{
								height: 32upx;
								line-height: 26upx;
								padding: 0 10upx;
								border: 2upx solid #96b8e0;
								font-size: 22upx;
								color: #0073ea;
								border-radius: 8upx;
							}
						}
					}
					.coupons{
						display: flex;
						flex-wrap: wrap;
						margin-top: 20upx;
						.item{
							height: 32upx;
							line-height: 26upx;
							border: 2upx solid #e7d2d0;
							background-color: #f8ecec;
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
					.nearby-busi{
						margin-top: 30upx;
						.title-box{
							display: flex;
							align-items: center;
							justify-content: space-between;
							.left{
								display: flex;
								align-items: center;
								image{
									width: 20upx;
									height: 20upx;
									margin-right: 12upx;
								}
								.text{
									font-size: 22upx;
									color: #000;
								}
							}
							.arrow{
								width: 18upx;
								height: 18upx;
								transition: all .5s;
								&.show{
									transform: rotate(-180deg);
								}
							}
						}
						.neb-busi-list{
							height: 0;
							overflow: hidden;
							transition: height .5s;
							&.show{
								height: auto;
							}
							.busi-item{
								height: 70upx;
								display: flex;
								align-items: center;
								justify-content: space-between;
								border-bottom: 2upx solid #f4f4f4;
								&:last-child{
									border-bottom: none;
								}
								.name{
									font-size: 24upx;
									color: #000;
								}
								.distance{
									font-size: 24upx;
									color: #565656;
								}
							}
						}
					}
				}
			}
		}
	}
	.filetr-dialog{
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		.inner{
			flex: 1;
			padding: 30upx;
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
