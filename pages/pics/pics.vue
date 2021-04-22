<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view @click="leftClick(index,item.id)" :class="active ===index?'active':''" v-for="(item,index) in pics"
				:key='item.id'>{{item.title}}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view class="item" v-for="item in images" :key="item.id">
				<image src="../../static/pic/11.jpg" @click="previewImg(item.img_url)"></image>
				<text>{{item.title}}</text>
			</view>
			<view v-if="images.length ===0 ">暂无数据</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pics: [],  //分类数据
				active: 0,
				images: []  //图片数据
			}
		},
		methods: {
			async getPicsCate() {
				const res = await this.$myRuquest({
					url: '/api/getimgcategory'
				})
				//console.log("获取分类数据",res.data.message)
				this.pics = res.data.message
				//获取左侧第一条数据,判断是否有数据
				if(this.images[0] != null){
					this.leftClick(0,this.images[0].id)
				}
			},
			async leftClick(index, id) {
				this.active = index;
				//获取右侧的数据
				//console.log(id)
				const res = await this.$myRuquest({
					url: '/api/getimages/' + id
				})
				console.log("返回数据是对象数组",res)
				this.images = res.data.message
			},
			//点击图片预览功能
			previewImg(current){
				//封装urls数组
				const urls = this.images.map(item=>{
					return item.img_url
				})
				console.log("图片预览",urls)
				uni.previewImage({
					current,
					urls
				})
			}
		},
		onLoad() {
			this.getPicsCate();
		}
	}
</script>

<style lang="scss">
	page {
		height: 100%;
	}

	.pics {
		height: 100%;
		display: flex;

		.left {
			width: 200rpx;
			height: 100%;
			/* 滚动条在左侧 */
			border-right: 1px solid #eee;

			view {
				height: 60px;
				line-height: 60px;
				color: #333333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;
			}

			.active {
				background: $shop-color;
				color: #FFFFFF;
			}
		}

		.right {
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;

			.item {
				image {
					width: 520rpx;
					height: 520rpx;
					border-radius: 10rpx;
				}
				text{
					font-size: 30rpx;
					line-height: 60rpx;
				}

			}

		}
	}
</style>
