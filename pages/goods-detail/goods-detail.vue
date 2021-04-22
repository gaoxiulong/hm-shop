<template>
	<view class="goods_detail">
		<!-- 轮播图 -->
		<swiper indicator-dots circular>
			<!-- 			<swiper-item v-for="(item,index) in swipers" :key="index">
				<image src="item.src"></image>
			</swiper-item> -->
			<swiper-item>
				<image src="../../static/pic/33.jpg"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/pic/44.jpg"></image>
			</swiper-item>
		</swiper>
		<view class="info">
			<view class="price">
				<text>¥{{detail.sell_price}}</text>
				<text>¥{{detail.market_price}}</text>
			</view>
			<view class="name">{{detail.title}}</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>货号：{{detail.goods_no}}</view>
			<view>库存：{{detail.stock_quantity}}</view>
		</view>
		<view class="line"></view>
		<view class="detail">
			<view class="title">商品介绍</view>
			<view class="content">
				<rich-text :nodes="content"></rich-text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 0,
				swipers: [],
				detail: {},
				content: ''
			}
		},
		methods: {
			//获取商品详情页的轮播图
			async getSwipers() {
				const res = await this.$myRuquest({
					url: '/api/getthumimages/' + this.id
				})
				//console.log(res)
				this.swipers = res.data.message
			},
			//获取商品详情
			async getDetailInfo() {
				const res = await this.$myRuquest({
					url: '/api/goods/getinfo/' +this.id
				})
				//console.log(res)
				this.detail = res.data.message[0]
			},
			//获取详情内容
			async getDetailContent() {
				const res = await this.$myRuquest({
					url: '/api/goods/getdesc/' +this.id
				})
				//console.log(res)
				this.content = res.data.message[0].content
			},


		},
		onLoad(options) {
			this.id = options.id;
			this.getSwipers()
			this.getDetailInfo()
			this.getDetailContent()
		}
	}
</script>

<style lang="scss">
	.goods_detail {
		swiper {
			height: 700rpx;

			image {
				height: 100%;
				width: 100%;
			}
		}

		.info {
			padding: 10rpx;

			.price {
				font-size: 38rpx;
				color: $shop-color;
				line-height: 80rpx;

				text:nth-child(2) {
					color: #C0C0C0;
					font-size: 28rpx;
					margin-left: 20rpx;
					text-decoration: line-through;
				}
			}

			.name {
				font-size: 32rpx;
				line-height: 60rpx;
			}
		}

		.line {
			height: 8rpx;
			width: 750rpx;
			background: #C0C0C0;
		}

		.box2 {
			padding: 0 10rpx;
			font-size: 32rpx;
			line-height: 70rpx;
		}

		.detail {
			.title {
				padding-left: 10rpx;
				font-size: 32rpx;
				line-height: 70rpx;
				border-bottom: 1px solid #eee;
			}

			.content {
				font-size: 28rpx;
				color: #333333;
				line-height: 50rpx;
			}
		}
	}
</style>
