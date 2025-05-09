<template>
	<view class="register">
		<form class="registerform"  @submit="onSubmit" >
			<view class="name">
				<p>姓名：</p>
				<input type="text" maxlength="10" placeholder="请输入您的姓名" class="input" name="name" />
			</view>
			<view class="IDcard">
				<p>校园卡号：</p>
				<input type="number" maxlength="12" placeholder="请输入您的校园卡号" class="input" name="Idcard" />
			</view>
			<view class="account">
				<p>账号：</p>
				<input type="text" maxlength="18" placeholder="请输入您将要使用的账号(18位以内)" class="input" name="account" />
			</view>
			<view class="password">
				<p>密码：</p>
				<input class="input" placeholder="请输入密码" :password="showPassword" name="password"  />
				<text class="uni-icon" :class="[!showPassword ? 'uni-eye-active' : '']"
					@click="changePassword">&#xe568;</text>
			</view>
			<!-- //能控制密码是否显示的密码输入框 -->
			<view class="passwordcheck">
				<p>再次输入密码：</p>
				<input class="input" placeholder="请再次输入密码" :password="showPassword" name="passwordcheck"  />
				<text class="uni-icon" :class="[!showPassword ? 'uni-eye-active' : '']"
					@click="changePassword">&#xe568;</text>
			</view>
			<view>
				<button  type="primary" class="button" form-type="submit" @click="clean" >提交</button>
			</view>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showPassword: true,
				search:'',
			}
		},
		methods: {
			//密码是否显示
			changePassword() {
				this.showPassword = !this.showPassword;
			},
			onSubmit(res){
				this.search = res.detail.value;
				console.log(this.search);
			},
			clean(){
				let that =this
				uni.request({
					url:'http://172.23.44.94:8000/register_test/test1',
					method:'POST',
					data:that.search,
						success: (res) => {
								console.log("请求成功", res);
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
	*{
		overflow: hidden;
	}
	.register{
		display: flex;
		justify-content: center;
	}
	.registerform{
		display: flex;
		justify-content: center;
		border-radius: 15px;
		box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
		background-image: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);
		border: solid 1rpx;
		padding: 40rpx;
		margin-top: 200rpx;
		.name{
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			.input{
				border: solid 1rpx;
				width: 850rpx;
				text-indent: 5px;
				border-radius: 2px;
			}
		}
		.IDcard{
			display: flex;
			flex-direction: row;
			margin-top: 40rpx;
			justify-content: space-between;
			.input{
				border: solid 1rpx;
				width: 850rpx;
				text-indent: 5px;
				border-radius: 2px;
			}
		}
		.account{
			display: flex;
			flex-direction: row;
			margin-top: 40rpx;
			justify-content: space-between;
			.input{
				border: solid 1rpx;
				width: 850rpx;
				text-indent: 5px;
				border-radius: 2px;
			}
		}
		.password{
			display: flex;
			flex-direction: row;
			margin-top: 40rpx;
			justify-content: space-between;
			.input{
				border: solid 1rpx;
				width: 850rpx;
				text-indent: 5px;
				border-radius: 2px;
			}
			.uni-icon{
				visibility: hidden;
				position: absolute;
			}
		}
		.passwordcheck{
			display: flex;
			flex-direction: row;
			margin-top: 40rpx;
			justify-content: space-between;
			.input{
				border: solid 1rpx;
				width: 850rpx;
				text-indent: 5px;
				border-radius: 2px;
			}
			.uni-icon{
				visibility: hidden;
				position: absolute;
			}
		}
		.button{
			margin-top: 40rpx;
			border: solid 1px;
			box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
		}
	}
</style>

