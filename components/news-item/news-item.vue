<template>
	<view>
		<view class="new_item" v-for="item in newsList" :key="item.id" @click="navigatorToDec(item.id)" >
			<image src="../../static/logo.png"></image>
			<!-- <image :src="item.img_url"></image> -->
			<view class="right" >
				<view class="tit">
					{{item.title}}
				</view>
				<view class="info">
					<text>发表：{{item.add_time|formatDate}} </text>
					<text>浏览：{{item.click}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: ['newsList'],  //接收夫组件传递过来的数据
		filters: {
			//格式化时间显示
			formatDate(date) {
				const newDate = new Date(date);
				const year =  newDate.getFullYear();
				const month = newDate.getMonth().toString().padStart(2,0)
				const day = newDate.getDay().toString().padStart(2,0)
				return year+ '-' +month+'-'+ day
			}
		},
		methods:{
			navigatorToDec(id){
				this.$emit('itemClick',id);
			}
		}
	} 
</script>

<style lang="scss">
	.new_item {
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid $shop-color;
	
		image {
			min-width: 200rpx;
			max-width: 200rpx;
			height: 150rpx;
		}
	
		.right {
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between; //以上三句实现上下分开显示对齐
	
			.tit {
				font-size: 30rpx;
			}
	
			.info {
				font-size: 24rpx;
	
				text:nth-child(2) {
					margin-left: 30rpx;
				}
			}
		}
	}
</style>
