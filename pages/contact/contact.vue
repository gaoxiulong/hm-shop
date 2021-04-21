<template>
	<view class="contact">
		<image src="../../static/pic/44.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：400-618-9090（点击拨打）</view>
			<view>公司地址：江苏省徐州市铜山区大学路1号中国矿业大学</view>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude" :markers="markers" :scale="scale"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: 117.15175,
				latitude: 34.220392,
				markers: [{
					longitude: 117.15175,
					latitude: 34.220392,
					iconPath: "../../static/pic/cumt.png",
					width: 40,
					height: 40
				}],
				scale: 15
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber: '400-618-9090'
				})
			}
			
		}
	}
</script>

<style lang="scss">
	.contact{
		image{
			width: 750rpx;
			height: 320rpx;
		}
		.info{
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view{
				line-height: 60rpx;
				border-bottom: 1px solid #eee;
			}
		}
		.map{
			width: 750rpx;
			height: 750rpx;
		}
	}

</style>
