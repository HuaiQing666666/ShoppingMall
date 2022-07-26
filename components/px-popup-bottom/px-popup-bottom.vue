<template>
	<view :class="['popup',{'popup-show':show}]" @mousewheel.prevent.stop @touchmove.stop.prevent
		:style="{'z-index':zindex}">
		<view class="mask" :style="{'z-index':maskZindex,bottom:bottom+'rpx'}" v-show="show" @click.stop="onClose"
			@touchmove.prevent.stop></view>
		<view :class="['content',{show}]" @click.stop @touchmove.prevent.stop :style="{height:`${height}px`,maxHeight:show ? cotMaxHeight:0,'border-top-right-radius':cotRadius,
			'border-top-left-radius':cotRadius,transition: `all ${animaTime}s ease-in`,bottom:bottom+'rpx','z-index':zindex}">
			<view id="title-bar" class="title-bar" v-show="title">
				<view class="title" :style="{fontWeight:fontweight}">{{title}}</view>
				<view class="close-wrap" @click.stop="onClose">
					<image class="close-icon" :src="closeIcon" mode="widthFix"></image>
				</view>
			</view>
			<view class="scroll-wrap">
				<scroll-view :class="{'scroll-view':isAnimaStart}" scroll-y="true" style="height:100%;"
					@scrolltolower="onScrollToLower">
					<view id="popup_content" class="popup_content">
						<slot></slot>
					</view>
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	import iconClose from '@/static/images/close40.png'
	export default {
		props: {
			title: { //标题
				type: String,
				default: ''
			},
			fontweight: {
				type: [String, Number],
				default: 'normal'
			},
			visible: { //隐藏显示标识
				type: Boolean,
				default: false
			},
			maxHeight: { //内容区域最大高度
				type: [String, Number],
				default: '75%'
			},
			radius: { //顶部圆角
				type: [String, Number],
				default: '0'
			},
			animaTime: { //弹窗动画时间
				type: Number,
				default: 0.2
			},
			bottom: { //离底部距离
				type: [String, Number],
				default: 0
			},
			zindex: {
				type: [String, Number],
				default: 1000
			},
			maskZindex: {
				type: [String, Number],
				default: 999
			},
			always: { //是否每次打开都重新计算内容高度
				type: Boolean,
				default: false
			},

		},
		data() {
			return {
				show: false,
				height: 0,
				PopHeight: 0,
				cotMaxHeight: '',
				isAnimaStart: false,
				rpxRate: "",
				cotRadius: 0,
				closeIcon: iconClose
			}
		},
		watch: {
			visible(newval) {
				this.isAnimaStart = true;
				setTimeout(() => {
					this.isAnimaStart = false;
				}, this.animaTime * 1000)

				if (newval && this.height === 0) {
					if (this.PopHeight === 0 || this.always) {
						this.setContViewHeight();

					} else {
						this.height = this.PopHeight
					}

					// #ifdef H5 
					this.setBodyOverFlow('hidden') //阻止滚动穿透
					//#endif
					this.$emit('open')

				} else {
					this.height = 0;
					// #ifdef H5 
					this.setBodyOverFlow('visible')
					//#endif

				}

				this.show = newval

			},
			maxHeight: {
				handler(newval) {
					this.cotMaxHeight = this.unitCheck(newval);

				},
				immediate: true
			},
			radius: {
				handler(newval) {
					this.cotRadius = this.unitCheck(newval);

				},
				immediate: true
			}
		},
		created() {
			this.rpxRate = this.getRpxRate()
		},
		mounted() {
			this.$nextTick(() => {
				// #ifdef H5
				this.preventTouch(document.querySelector(
					'.scroll-wrap .uni-scroll-view .uni-scroll-view')); //防止浏览器报错
				//#endif
			})
		},
		methods: {
			onClose() {
				this.$emit("update:visible", false);
				this.$emit('close')
			},
			//触底
			onScrollToLower(e) {
				this.$emit("reachBottom");
			},
			getRpxRate() {
				let res = uni.getSystemInfoSync();
				let width = res.windowWidth;
				let rate = 750.00 / width;
				return rate
			},
			unitCheck(value) {
				const val = String(value);
				if (!val.includes('px') && !val.includes('%')) {
					return `${val}rpx`;
				}
				return val;

			},
			preventTouch(el) {
				el.addEventListener('touchmove', function(e) {
					e.stopPropagation();

				}, {
					passive: false
				});
			},
			setBodyOverFlow(val) {
				document.body.style.overflow = val
			},

			//设置内容区域高度
			async setContViewHeight() {
				let data = await this.computeHeight();
				this.height = data.height + (this.title ? 100 / parseFloat(this.rpxRate) : 0);
				this.PopHeight = this.height;
			},
			//计算内容区域高度
			computeHeight() {
				return new Promise(resolve => {
					this.$nextTick(() => {
						const query = uni.createSelectorQuery().in(this);
						query.select('#popup_content').boundingClientRect(data => {
							resolve(data)
						}).exec();
					})
				})
			}

		}


	}
</script>

<style lang="scss" scoped>
	.popup {

		&.popup-show {
			position: fixed;
			top: 0;
			right: 0;
			left: 0;
			bottom: 0;
			overflow: hidden;
			z-index: 999;
		}

		.mask {
			position: fixed;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
			background-color: rgba($color: #000000, $alpha: 0.5);
			z-index: 999;
		}

		.content {
			position: fixed;
			bottom: 0;
			left: 0;
			right: 0;
			height: 0;
			height: auto;
			background-color: white;
			transition: all 0.2s ease-in;
			z-index: 1000;
			display: flex;
			flex-direction: column;
			align-items: center;
			overflow: hidden;

			.title-bar {
				width: 100%;
				flex-shrink: 0;
				text-align: center;
				position: relative;
				padding: 25rpx 70rpx 0;
				box-sizing: border-box;
				height: 100rpx;

				.title {
					font-size: 34upx;
					font-family: PingFang SC;
					font-weight: bold !important;
					color: #111111;
					width: 100%;
					overflow: hidden;
					text-overflow: ellipsis;
					white-space: nowrap;
				}

				.close-wrap {
					position: absolute;
					top: 20rpx;
					right: 10rpx;
					padding: 10rpx 20rpx;
					box-sizing: border-box;
				}

				.close-icon {
					width: 40rpx;
					height: 40rpx;
				}
			}

			.scroll-wrap {
				flex: 1;
				height: 0;
				width: 100%;
			}

			&.visible {
				max-height: 75%;
				overflow-y: hidden;
				height: auto;

			}
		}
	}

	.scroll-view ::-webkit-scrollbar {
		display: none !important;
		width: 0 !important;
		height: 0 !important;
		-webkit-appearance: none;
		background: transparent;

	}

	.popup_content {
		width: 100%;
		padding: 30rpx;
		box-sizing: border-box;

		&::after {
			display: block;
			width: 100%;
			content: "\00A0";
			overflow: hidden;
			opacity: 0;
			height: 1rpx;
		}

	}
</style>
