<template>
	<view class="all">
		<!-- 统一导航栏 -->
		<view class="topbar">
			<view class="leftlabel">
				<view class="text1">购物车</view>
				<view class="text1">|</view>
				<view class="text">商品分类</view>
			</view>
			<view class="rightlabel">
				<view class="text1">我</view>
				<view class="text1">|</view>
				<view class="text">消息</view>
				<view class="text1">|</view>
				<view class="text">收藏</view>
				<view class="text1">|</view>
				<view class="text">历史记录</view>
				<view class="text1">|</view>
				<view class="text">联系客服</view>
				<view class="text1">|</view>
				<view class="text">发布</view>
			</view>
		</view>
		<view class="bgpic">
			
		</view>
		
		<!-- 搜索栏 -->
		<view class="search">
			<!-- 左边图片 -->
			<view class="leftpic">
				<img src="../../static/logo.png"/>
			</view>
			<!-- 中间搜索框 -->
			<view class="searchbar">
				<!-- 上端的分区 -->
				<view class="">
				</view>
				<!-- 中间的搜索 -->
				<view class="searchItem">
					<form @submit="onSubmit">
						<view class="form">
							<input  class="input" type="text" maxlength="20" placeholder="请输入搜索内容" name="searchsomething" />
							<button class="button"  form-type="submit"  type="primary" >搜索</button>
						</view>
					</form>
				</view>
				<!-- 下端的今日推荐 -->
				<view class="">
				</view>
			</view>
			<!-- 右边图片 -->
			<view class="rightpic">
				<img src="../../static/logo.png"/>
			</view>
		</view>
		<view class="body">
			<view class="label">
<!-- 				<li>二手交易</li>
				<li>表白墙</li>
				<li>校园吐槽</li>
				<li>招聘信息</li> -->
			</view>
			<view class="swiperbar">
				<view class="ad">
					
				</view>
				<view class="swiper">
					
				</view>
				<view class="person">
					
				</view>
			</view>
			<view class="more">
				
			</view>
		</view>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				search:'',
				result:'',
				goods:[],
			}
		},
		methods: {
			onSubmit(res){
				console.log(res)
				this.search = res.detail.value.searchsomething
				let that =this
				uni.request({
					url:'http://172.23.103.128:8000/search/test4',
					method:'POST',
					data:that.search,
						success: (res) => {
								console.log("请求成功", res);
								that.result = res;
								let string1 = this.result.data.match
								uni.navigateTo({
									url:'../pagelist/pagelist?a=' + string1 
									})
							},
						fail: (err) => {
							console.error("请求失败", err);
							},
				});
			},
		}
	}
</script>

<style lang="scss">
	.all{
		display: flex;
		flex-direction: column;
		width: 100vw;
	}
	.bgpic{
		background-image: url('/static/searchbackground.jpg');
		background-size: cover;
		height: 70px;
		width: 100vw;
	}
	.topbar{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		border-bottom: #9C9C9C 1px dotted;
		padding: 5px;
		.leftlabel{
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			margin-left: 10px;
			.text{
				margin-left: 10px;
				color: #9C9C9C;
			}
			.text1{
				margin-left: 10px;
				color: #9C9C9C;
			}
		}
		.rightlabel{
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			margin-right: 15px;
			.text{
				margin-left: 10px;
				color: #9C9C9C;
			}
			.text1{
				margin-left: 10px;
				color: #9C9C9C;
			}
			
		}
	}
	.search{
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		width: 100vw;
		height: 20vh;
		.searchbar{
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			width: 60vw;
			height: 15vh;

			.searchItem{
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				height: 15vh;
				width: 60vw;
				.form{
					height: 15vh;
					width: 50vw;
					display: flex;
					flex-direction: row;
					justify-content: center; 
					align-items: center;
					.button{
						border: solid 1px;
						box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
					}
					.input{
						width: 700rpx;
						text-indent: 1em;
						border: solid 1rpx;
						border-radius: 10px;
						height: 10vh;
						margin-left: 50px;	
					}
				}
			}
		}
	}
</style>
