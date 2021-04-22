<template>
	<view class="news_detail">
		<text class="title">{{detail.title}}</text>
		<view class="info">
			<text>发布时间：{{detail.add_time | formatDate}}</text>
			<text>浏览：{{detail.click}}</text>
		</view>
		<view class="contact">
			<!-- 使用富文本 -->
			<rich-text :nodes="detail.content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 0,
				detail: {}
			}
		},
		methods: {
			//获取详情页数据
		async getNewsDetail(){
				const res = await this.$myRuquest({
					url: '/api/getnew/'+this.id
				})
				//console.log("返回详情数据",res)
				this.detail = res.data.message[0]
			}
			
		},
		onLoad(options) {
			//console.log(options) //获取id数据
			this.id = options.id
			this.getNewsDetail()
		}
	}
</script>

<style lang="scss">
.news_detail{
	font-size: 30rpx;
	padding: 0 20rpx;
	.title{
		width: 100%;
		display: block;
		text-align: center;
		margin: 20rpx auto;
		text-shadow: 1px 0px #000  /* 标题加粗效果*/
	}
	.info{
		display: flex;
		justify-content: space-between;
	}
	.contact{
		
	}
}

</style>
