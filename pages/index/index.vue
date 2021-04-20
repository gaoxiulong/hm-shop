<template>
	<view class="home">
		<swiper autoplay circular indicator-dots interval="2000">
			<swiper-item v-for="item in swiper" :id="item.id">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
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
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiper: []
			}
		},
		onLoad() {
			this.getSwiper()
		},
		methods: {
			async getSwiper() {
				console.log("我被触发了")
				const res = await this.$myRuquest({
					url: '/api/getlunbo'
				})
				//获取轮播图
				this.swiper = res.data.message
			}

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
	}

	.nav {
		display: flex;

		.nav_item {
			width: 25%;
			text-align: center;

			view {
				width: 120rpx;
				height: 120rpx;
				background: #b50e03;
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
</style>
