<template>
	<view class="all">
		<!-- 各个页面统一的bar -->
		<view class="bar">	
				
		</view>
		<!-- 网页头部的背景图片 -->
		<view class="backgroundpicture">
			
		</view>
		<!-- 页面的主体部分 -->
		<view class="mainbody">
			<!-- 左边是广告图片 -->
			<view class="left">
				<img src="../../static/logo.png" alt="" class="leftimg" />
			</view>
			<!-- 右边是登录注册界面 -->
			<view class="right">
				<!-- 登录的页面 -->
				<view class="login">
						<form class="form" @submit="onSubmit">
							<view class="account">
								<p>账号：</p>
								<input  class="input" type="text" maxlength="20" placeholder="请输入您的账号" name="account" />
							</view>
							<view class="password">
								<p>密码： </p>
								<input class="input" placeholder="请输入密码" :password="showPassword" name="password"  />
								<text class="uni-icon" :class="[!showPassword ? 'uni-eye-active' : '']"
									@click="changePassword">&#xe568;</text>
							</view>
							<view class="buttons">
								<button class="button"  form-type="submit"  type="primary" >登录</button>
								<button class="button" @click="pagechangetoregister">注册</button>
							</view>
						</form>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showPassword: true,
				search:''
			}
		},
		onLoad() {

		},
		methods: {
			changePassword() {
				this.showPassword = !this.showPassword;
			},
			onSubmit(e){
				console.log(e)
				this.search = e.detail.value.searchBar
			},
			pagechangetoregister(){
				uni.navigateTo({
					url:'/pages/register/register'
				})
			},
		}
	}
</script>

<style lang="scss">
	.all{
		display: flex;
		flex-direction: column;
		.bar{
			width: 100vw;
			height: 5vh;
		}
		.backgroundpicture{
			width: 100vw;
			height: 15vw;
		}
	}
	.mainbody{
		display: flex;
		flex-direction: row;
		.left{
			justify-content: center;

			width: 100%;
			display: flex;
			.leftimg{
				justify-content: center;
				align-items: center;
			}
		}
		.right{
			width: 50vw;
			margin: auto;
			.login{
				display: flex;
				width: 40vw;
				border: solid 1rpx;
				margin-right: 50rpx;
				padding: 40rpx;
				.form{
					display: flex;
					margin: 10rpx;
					padding: 10rpx;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					margin-left: auto;
					margin-right: auto;
					.account{
						display: flex;
						flex-direction: row;
						justify-content: center;
						align-items: center;
					}
					.password{
						margin-top: 20rpx;
						display: flex;
						flex-direction: row;
						justify-content: center;
						align-items: center;
						position: relative;
						.uni-icon{
							position: absolute;
							right: 10rpx;
							visibility: hidden;
						}
					}
					.buttons{
						display: flex;
						flex-direction: row;
						align-items: center;
						margin-top: 40rpx;
						.button{
							border: solid 1px;
							box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
						}
					}
			}
		}
	}

	}
	.input{
		width: 350px;
		text-indent: 1em;
		border: solid 1rpx;
		border-radius: 10px;
		height: 40px;
		line-height: 40px;
	}
</style>
