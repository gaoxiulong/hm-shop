<template>
	<view class="goods_list">
		<goods-list :goods='goods' @goodItemClick="goGoodDetail"></goods-list>
		<view class="isOver" v-if="flag">---------END---------</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				goods: [],
				pageindex: 1,
				flag: false
			}
		},
		methods: {
			//获取商品数据
			async getHotGoods(callback) {
				const res = await this.$myRuquest({
					url: '/api/getgoods?pageindex=' + this.pageindex
				})
				//console.log("我被触发了", res)
				this.goods = [...this.goods, ...res.data.message];
				callback && callback()  //下拉刷新回调
			},
			//获取商品详情
			goGoodDetail(id){
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id='+id
				})
			}

		},
		onLoad() {
			this.getHotGoods()  //无回调的调用
		},
		components: {
			"goods-list": goodsList
		},
		//上拉加载更多功能，默认开启
		onReachBottom() {
			console.log("我触底了",this.goods.length)
			//判断是否还有数据
			if (this.goods.length < this.pageindex * 10) {
				return this.flag = true
			} else {
				this.pageindex++;
				this.getHotGoods();
			}
		},
		//下拉刷新功能，pages页手动开启该功能
		onPullDownRefresh() {
			console.log("下拉刷新了")
			this.pageindex = 1
			this.goods = []
			this.flag = false
			setTimeout(()=>{
				this.getHotGoods(()=>{
					uni.stopPullDownRefresh()  //停止下拉刷新
				})
			},1000)
		}
	}
</script>

<style lang="scss">
	.goods_list {
		background: #C0C0C0;

		.isOver {
			color: #333333;
			text-align: center;
			width: 100%;
			height: 50rpx;
			line-height: 50rpx;
			font-size: 28rpx;
		}
	}
</style>
