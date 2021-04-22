<template>
	<view class="goods_list">
		<view class="goods_item" v-for="item in goods" :id="item.id" @click="goodItemClick(item.id)">
			<image src="../../static/pic/66.jpg"></image>
			<view class="price">
				<text>¥{{item.sell_price}}</text>
				<text>¥{{item.market_price}}</text>
			</view>
			<view class="name">{{item.title}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: ['goods'],
		methods:{
			goodItemClick(id){
				this.$emit('goodItemClick',id)
			}
		}
	} 
</script>

<style lang="scss">
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
</style>
