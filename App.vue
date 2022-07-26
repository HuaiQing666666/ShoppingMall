<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
			// 获取手机信息，适配iphone底部
			let bottomBlackLineHeight = 0 // iphoneX底部一条黑线，有些页面要避开
			const mobileInfo = uni.getSystemInfoSync();
			let iphoneXArr = ["iPhone X", "iPhone 11", "iPhone 11 Pro Max"];
			iphoneXArr.forEach(function(item) {
				if (mobileInfo.model.search(item) !== -1) {
					bottomBlackLineHeight = 40;
				}
			});
			uni.setStorageSync('bottomBlackLineHeight', bottomBlackLineHeight)
			
			uni.getSystemInfo({
				success: (result) => {
					uni.setStorageSync('statusBarHeight', result.statusBarHeight)
				},
				fail: (error) => {
					console.log(error)
				}
			})
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import "@/uni_modules/uview-ui/index.scss";
	view{
		box-sizing: border-box;
	}
	.ellipsis{
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	.ellipsis2{
		overflow:hidden; 
		text-overflow:ellipsis;
		display:-webkit-box; 
		-webkit-box-orient:vertical;
		-webkit-line-clamp:2; 
	}
	
	// 猜你喜欢样式
	.like-box{
		display: flex;
		align-items: center;
		justify-content: center;
		image{
			width: 40upx;
		}
		.text{
			font-size: 28upx;
			color: #000;
			font-weight: bold;
			margin: 0 10upx;
		}
	}
	
	// 商品列表
	.goods-list{
		box-sizing: border-box;
		width: 100%;
		column-count: 2; //  2列
		column-width: calc(50% - 8upx); // 每一列宽度
		column-gap: 16upx; // 列间距
		margin-top: 20upx;
		.item{
			box-sizing: border-box;
			background-color: #fff;
			border-radius: 20upx;
			overflow: hidden;
			margin-bottom: 16upx;
			overflow: hidden;
			break-inside: avoid;
			.img-box{
				width: 100%;
				height: 340upx;
				position: relative;
				overflow: hidden;
				image{
					width: 100%;
					height: 100%;
				}
				.act-title{
					width: 45%;
					height: 52upx;
					line-height: 52upx;
					border-radius: 0 10upx 0 0;
					text-align: center;
					font-size: 24upx;
					color: #d25c45;
					background-color: #fff5e3;
					position: absolute;
					left: 0;
					bottom: 0;
					z-index: 10;
				}
				.act-num{
					width: 55%;
					height: 40upx;
					line-height: 40upx;
					text-align: center;
					font-size: 24upx;
					color: #fff;
					font-weight: bold;
					background-color: #ff3170;
					position: absolute;
					right: 0;
					bottom: 0;
					z-index: 10;
				}
			}
			.info-box{
				padding: 0 16upx;
				.goods-name{
					font-size: 24upx;
					color: #000;
					line-height: 1.4;
					margin: 10upx 0;
				}
				.offers{
					display: flex;
					align-items: center;
					flex-wrap: wrap;
					margin-bottom: 8upx;
					.item{
						box-sizing: border-box;
						flex-shrink: 0;
						height: 32upx;
						line-height: 32upx;
						display: flex;
						align-items: center;
						padding: 0 10upx;
						border: 1px solid #ee93a5;
						border-radius: 10upx;
						font-size: 18upx;
						color: #bc1428;
						margin-right: 8upx;
						margin-bottom: 8upx;
					}
				}
				.price{
					margin-top: 8upx;
					font-size: 26upx;
					color: #ff201f;
					font-weight: bold;
				}
				.shop-info{
					padding: 14upx 0;
					margin-top: 10upx;
					border-top: 1px solid #f6f6f6;
					display: flex;
					align-items: center;
					.logo{
						flex-shrink: 0;
						width: 56upx;
						height: 56upx;
						border: 1px solid #f6f6f6;
						border-radius: 10upx;
						margin-right: 8upx;
						overflow: hidden;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.inner{
						width: calc(100% - 64upx);
						.name{
							font-size: 24upx;
							color: #000;
						}
						.freight{
							font-size: 20upx;
							color: #5c5c5c;
							margin-top: 6upx;
						}
					}
				}
			}
		}
	}
	
	
	// 重置复选框样式
	checkbox .wx-checkbox-input{
		box-sizing: border-box !important;
		width: 30rpx !important;
		height: 30rpx !important;
		border-radius: 50%;
		border: 2rpx solid #C9CED6 !important;
	}
	checkbox .wx-checkbox-input.wx-checkbox-input-checked {
		background: #00cb29 !important;
		border: 2rpx solid #00cb29 !important;
	}
	checkbox .wx-checkbox-input.wx-checkbox-input-checked::before {
		color: #ffffff !important;
		font-size: 24upx !important;
	}
	
	
</style>
