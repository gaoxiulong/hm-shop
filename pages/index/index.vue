<template>
	<view class="home">
		<!-- 轮播图 -->
		<swiper autoplay circular indicator-dots interval="2000">
			<swiper-item v-for="item in swiper" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		<!-- 导航 -->
		<view class="nav">
			<view class="nav_item">
				<view class="iconfont icon-ziyuan"></view>
				<text>黑马资源</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-guanyuwomen"></view>
				<text>关于我们</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-tupian"></view>
				<text>社区图片</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-shipin"></view>
				<text>视频学习</text>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<view class="goods_list">
				<view class="goods_item" v-for="item in goods" :id="item.id">
					<image src="../../static/pic/66.jpg"></image>
					<view class="price">
						<text>¥{{item.sell_price}}</text>
						<text>¥{{item.market_price}}</text>
					</view>
					<view class="name">{{item.title}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiper: [],
				goods: []
			}
		},
		onLoad() {
			this.getSwiper()
			this.getHotGoods()
		},
		methods: {
			async getSwiper() {
				const res = await this.$myRuquest({
					url: '/api/getlunbo'
				})
				//获取轮播图
				this.swiper = res.data.message
			},
			async getHotGoods() {
				const res = await this.$myRuquest({
					url: '/api/getgoods?pageindex=1'
				})
				//获取商品数据
				console.log("我被触发了", res)
				this.goods = res.data.message;
			},

		}
	}
</script>

<style lang="scss">
	.home {
		swiper {
			width: 750rpx;
			height: 380rpx;

			image {
				height: 100%;
				width: 100%;
			}
		}


		.nav {
			display: flex;

			.nav_item {
				width: 25%;
				text-align: center;

				view {
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 60rpx;
					margin: 10px auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}

				.icon-tupian {
					font-size: 45rpx;
				}

				text {
					font-size: 30rpx;
				}
			}
		}

		.hot_goods {
			background: #eee;
			overflow: hidden;
			/* 子元素设置阻止冒泡 */
			margin: 10px 0;

			.tit {
				height: 50px;
				line-height: 50px;
				text-align: center;
				letter-spacing: 20px;
				color: $shop-color;
				background: #FFFFFF;
				margin: 5px 0;
			}

			.goods_list {
				padding: 0px 15rpx;
				display: flex;
				/* 一行显示 */
				flex-wrap: wrap;
				/* 换行 */
				justify-content: space-between;

				/* 两个商品中间有空隙*/
				.goods_item {
					background: #FFFFFF;
					width: 355rpx;
					margin: 10rpx 0;
					/* 设置上下边距 */
					padding: 15rpx;
					box-sizing: border-box;

					/* 盒子尺寸不变*/
					image {
						width: 90%;
						height: 150px;
						display: block;
						/* 让图片居中生效*/
						margin: 0 auto;
						
					}

					.price {
						color: $shop-color;
						font-size: 36rpx;
						margin: 10rpx 0;
						text:nth-child(2) {
							color: #C0C0C0;
							font-size: 28rpx;
							margin-left: 20rpx;
							text-decoration: line-through;
						}
					}

					.name {
						font-size: 30rpx;
						line-height: 50rpx;
						padding-top: 10rpx;
						padding-bottom: 15rpx;
					}
				}
			}
		}
	}
</style>
