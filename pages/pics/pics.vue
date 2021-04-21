<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view @click="leftClick(index)" :class="active ===index?'active':''" v-for="(item,index) in pics" :key='item.id'>{{item.title}}</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pics: [],
				active: 0
			}
		},
		methods: {
		async getPicsCate() {
			const res = await this.$myRuquest({
					url: '/api/getimgcategory'
				})
				//console.log("获取分类数据",res.data.message)
				this.pics = res.data.message
			},
			leftClick(index){
				this.active = index;
			}
		},
		onLoad() {
			this.getPicsCate();
		}
	}
</script>

<style lang="scss">
page{
	height: 100%;
}
.pics{
	height: 100%;
	.left{
		width: 200rpx;
		height: 100%;/* 滚动条在左侧 */
		border-right: 1px solid #eee;
		view{
			height: 60px;
			line-height: 60px;
			color: #333333;
			text-align: center;
			font-size: 30rpx;
			border-top: 1px solid #eee;
		}
		.active{
			background: $shop-color;
			color: #FFFFFF;
		}
	}
}

</style>
