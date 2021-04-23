<template>
	<view class="video">
		<view class="video_item">
			<video src="../../static/video/earth.mp4" controls></video>
			<view class="title">
				第一章：GIS与数字地球1
			</view>
		</view>
		<view class="video_item">
			<video src="../../static/video/earth.mp4" controls></video>
			<view class="title">
				第二章：GIS与数字地球2
			</view>
		</view>
		<view class="video_item">
			<video src="../../static/video/earth.mp4" controls></video>
			<view class="title">
				第三章：GIS与数字地球3
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.video {
		.video_item {
			width: 750rpx;
			display: flex;
			flex-direction: column;

			video {
				width: 100%;
			}

			.title {
				width: 100%;
				text-align: center;/* 居中 */
				font-size: 34rpx;
				color: $shop-color;
				line-height: 60rpx;
			}
		}
	}
</style>
