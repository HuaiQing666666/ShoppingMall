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
				<text class="text">休闲食品</text>
				<view class="search-box">
					<image class="img" src="../../static/images/icon_search.png" mode="heightFix"></image>
					<text class="text">关键词</text>
				</view>
			</view>
		</view>
		<view :class="fixedTop?'content-inner top-fixed':'content-inner'">
			<!-- 分类 -->
			<scroll-view :class="fixedCate?'fixed-cate-scroll':''" scroll-x="true" :style="{top: statusBarHeight + 44 +'px'}">
				<view class="cate-list">
					<view v-for="(item,index) in 10" :key="index" :class="activeCate == index?'item active':'item'" @click="choseCate(index)">
						<view class="img-box">
							<image src="../../static/logo.png" mode="aspectFill"></image>
						</view>
						<view class="text">糖巧果冻</view>
					</view>
				</view>
			</scroll-view>
			<!-- 子分类 -->
			<view class="sub-cate-box">
				<view v-for="(item,index) in 9" :key="index" :class="subActiveCate == index?'item active':'item'" @click="choseSubCate(index)">黑巧克力</view>
			</view>
			<!-- 商品列表 -->
			<view :class="fixedCate?'goods-list cate-fixed':'goods-list'">
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
				fixedTop: false, // 是否固定头部搜索框
				fixedCate: false, // 是否固定分类
				statusBarHeight: uni.getStorageSync('statusBarHeight'),
				scrollTop: 0,
				activeCate: 0, // 选中的分类
				subActiveCate: 0, // 选中的子分类
			}
		},
		methods: {
			scroll(e) {
				console.log(e.detail.scrollTop)
				if(e.detail.scrollTop >= 10) {
					this.fixedTop = true
				} else {
					this.fixedTop = false
				}
				if(e.detail.scrollTop >= 80) {
					this.fixedCate = true
				} else {
					this.fixedCate = false
				}
			},
			// 返回上一页
			goBack() {
				uni.navigateBack({
					delta:1,
				})
			},
			// 分类选择
			choseCate(index) {
				this.activeCate = index
			},
			// 子分类选择
			choseSubCate(index) {
				this.subActiveCate = index
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
	.content{
		height: 100%;
		position: relative;
		.top-cont{
			background-color: #f5b70a;
			transition: all .5s;
			&.fixed{
				width: 100%;
				background-color: #fff;
				position: fixed;
				top: 0;
				left: 0;
				z-index: 999;
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
					margin-left: 20upx;
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
			}
		}
		.content-inner{
			padding: 0 20upx;
			background-color: #f6f6f6;
			border-radius: 20upx 20upx 0 0;
			position: relative;
			&.top-fixed{
				padding-top: 88upx;
			}
			&::after{
				content: "";
				width: 100%;
				height: 20upx;
				background-color: #f5b70a;
				position: absolute;
				top: 0;
				left: 0;
				z-index: -1;
			}
			// 分类固定
			.fixed-cate-scroll{
				width: 100%;
				background-color: #fff;
				position: fixed;
				left: 0;
				z-index: 999;
				.cate-list{
					flex-wrap: nowrap;
				}
			}
			.cate-list{
				display: flex;
				flex-wrap: wrap;
				padding-top: 16upx;
				
				.item{
					flex-shrink: 0;
					width: 20%;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					margin-bottom: 25upx;
					.img-box{
						box-sizing: border-box;
						width: 90upx;
						height: 90upx;
						border-radius: 50%;
						overflow: hidden;
						margin-bottom: 10upx;
						image{
							width: 100%;
							height: 1005;
						}
					}
					.text{
						width: 114upx;
						height: 36upx;
						line-height: 36upx;
						border-radius: 18upx;
						text-align: center;
						font-size: 22upx;
						color: #000;
					}
					&.active{
						.img-box{
							border: 4upx solid #f5b300;
						}
						.text{
							background: #fab706;
							color: #fff;
						}
					}
				}
			}
			.sub-cate-box{
				padding: 20upx;
				padding-bottom: 0;
				background-color: #fff;
				border-radius: 20upx;
				display: flex;
				flex-wrap: wrap;
				.item{
					width: 23.5%;
					height: 60upx;
					line-height: 60upx;
					text-align: center;
					margin-right: 2%;
					font-size: 22upx;
					color: #6a6a6a;
					background-color: #f4f4f4;
					border-radius: 30upx;
					margin-bottom: 20upx;
					&:nth-child(4n) {
						margin-right: 0;
					}
					&.active{
						background-color: #fef3d7;
						color: #f0b91e;
						font-weight: bold;
					}
				}
			}
			.goods-list.cate-fixed{
				padding-top: 168upx;
			}
		}
	}

</style>
