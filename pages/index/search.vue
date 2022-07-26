<template>
	<view class="content">
		<view class="top-cont" :style="{paddingTop: statusBarHeight +'px'}">
			<view class="inner">
				<image class="back" src="../../static/images/icon_back_b.png" mode="heightFix" @click="back"></image>
				<view class="screen-box">
					<image class="search" src="../../static/images/icon_search.png" mode=""></image>
					<input type="text" placeholder="搜索附近的商家、商品" placeholder-style="font-size:26rpx;color:#DADADA;">
					<text class="text" @click="toSearchList">搜索</text>
				</view>
			</view>
		</view>
		<view class="cont-inner">
			<!-- 搜索历史 -->
			<view class="search-info">
				<view class="title-box">
					<view class="title">搜索历史</view>
					<view class="btn">清除搜索历史</view>
				</view>
				<view class="search-list">
					<view v-for="(item,index) in 6" :key="index" class="item ellipsis">
						<text class="text">四个字</text>
					</view>
					<view class="item ellipsis">
						<text class="text">名字很长很长很长很长很长很长很长很长</text>
					</view>
				</view>
			</view>
			<!-- 热门搜索 -->
			<view class="search-info">
				<view class="title-box">
					<view class="title">热门搜索</view>
				</view>
				<view class="search-list">
					<view class="item ellipsis hot">
						<image class="img" src="../../static/images/icon_hot.png" mode=""></image>
						<text class="text">鸡蛋</text>
					</view>
					<view v-for="(item,index) in 6" :key="index" class="item ellipsis">四个字</view>
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
			}
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			toSearchList() {
				uni.redirectTo({
					url: './searchList'
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
</style>
<style scoped lang="scss">
	.content{
		height: 100%;
		display: flex;
		flex-direction: column;
		.top-cont{
			background-color: #f6f6f6;
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
					justify-content: space-between;
					padding: 0 20upx;
					.search{
						width: 30upx;
						height: 30upx;
						margin-right: 12upx;
					}
					input{
						flex: 1;
						font-size: 26upx;
						color: #000;
					}
					.text{
						font-size: 26upx;
						color: #000;
						margin-left: 12upx;
					}
				}
			}
		}
		.cont-inner{
			flex: 1;
			background-color: #fff;
			border-radius: 20upx 20upx 0 0;
			padding: 0 25upx;
			.search-info{
				padding-top: 20upx;
				.title-box{
					padding: 20upx 0;
					display: flex;
					align-items: center;
					justify-content: space-between;
					.title{
						font-size: 28upx;
						color: #000;
						font-weight: bold;
					}
					.btn{
						font-size: 24upx;
						color: #575757;
					}
				}
				.search-list{
					display: flex;
					flex-wrap: wrap;
					.item{
						max-width: 250upx;
						height: 54upx;
						line-height: 54upx;
						padding: 0 20upx;
						border-radius: 27upx;
						margin: 0 20upx 15upx 0;
						background-color: #f4f4f4;
						display: flex;
						align-items: center;
						&.hot{
							background-color: #fef0f0;
						}
						.img{
							width: 26upx;
							height: 26upx;
							margin-right: 10upx;
						}
						.text{
							font-size: 22upx;
							color: #363636;
						}
					}
				}
			}
		}
	}

</style>
