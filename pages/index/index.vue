<template>
	<view class="home">
		<swiper autoplay circular indicator-dots interval="2000" >
			<swiper-item v-for="item in swiper" :id="item.id" >
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		<view class="nav">
			
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
</style>
