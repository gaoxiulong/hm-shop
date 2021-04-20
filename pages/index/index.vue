<template>
	<view class="home">
		<swiper autoplay circular indicator-dots interval="2000" >
			<swiper-item v-for="item in swiper" :id="item.id" >
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
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
			getSwiper() {
				console.log("我被触发了")
				uni.request({
					url: 'http://localhost:8082/api/getlunbo',
					success:res=> {
						console.log(res)
						this.swiper = res.data.message
					}
				})
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
