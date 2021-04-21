<template>
	<view class="goods_list">
		<goods-list :goods='goods'></goods-list>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				goods: [],
				pageindex: 1
			}
		},
		methods: {
			//获取商品数据
			async getHotGoods() {
				const res = await this.$myRuquest({
					url: '/api/getgoods?pageindex='+this.pageindex
				})
				//console.log("我被触发了", res)
				this.goods = res.data.message;
			}
			
		},
		onLoad() {
			this.getHotGoods()
		},
		components:{
			"goods-list": goodsList
		},
		onReachBottom() {
			console.log("我触底了")
		}
	}
</script>

<style lang="scss">
	.goods_list{
		background: #C0C0C0;
	}

</style>
