<template>
	<view class="home">
		<swiper autoplay circular indicator-dots interval="2000">
			<swiper-item>
				<image src="../../static/pic/11.jpg"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/pic/22.jpg"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/pic/33.jpg"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/pic/44.jpg"></image>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

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
</style>
