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
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list :goods= 'goods'></goods-list>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				swiper: [],
				goods: [],
				navs: [{
					icon: 'iconfont icon-ziyuan',
					title: '黑马超市',
					path: '/pages/goods/goods'
				},
				{
					icon: 'iconfont icon-guanyuwomen',
					title: '关于我们',
					path: '/pages/contact/contact'
				},
				{
					icon: 'iconfont icon-tupian',
					title: '社区图片',
					path: '/pages/pics/pics'
				},
				{
					icon: 'iconfont icon-shipin',
					title: '视频学习',
					path: '/pages/videos/videos'
				}
				]
			}
		},
		onLoad() {//加载轮播图和商品列表数据
			this.getSwiper()
			this.getHotGoods()
		},
		methods: {
			//获取轮播图
			async getSwiper() {
				const res = await this.$myRuquest({
					url: '/api/getlunbo'
				})

				this.swiper = res.data.message
			},
			//获取商品数据
			async getHotGoods() {
				const res = await this.$myRuquest({
					url: '/api/getgoods?pageindex=1'
				})
				console.log("我被触发了", res)
				this.goods = res.data.message;
			},
			//导航跳转
			navItemClick(url) {
				console.log("跳转",url)
				uni.navigateTo({
					url
				})
			}

		},
		components:{
			"goods-list": goodsList
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
		}
	}
</style>
