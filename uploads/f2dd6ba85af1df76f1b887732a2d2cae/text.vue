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
		<view class="label">
			<view class="text">生活用品</view>
			<view class="text1">|</view>
			<view class="text">学习资料</view>
			<view class="text1">|</view>
			<view class="text">模玩周边</view>
			<view class="text1">|</view>
			<view class="text2">户外运动</view>
		</view>
		<view class="publish-container">
		  <view class="upload-container">
		    <button class="upload-button" @click="chooseImage">点击上传图片</button>
		    <image class="uploaded-image" :src="imageSrc" v-if="imageSrc"></image>
		  </view>
		  
		  <view class="input-group">
		    <input type="text" v-model="price" placeholder="填写价格" class="input-field" />
		  </view>
		  
		  <view class="input-group">
		    <textarea v-model="description" placeholder="填写商品描述" class="textarea-field"></textarea>
		  </view>
		  
		  <view class="input-group">
		    <picker mode="selector" :range="themes" v-model="selectedTheme" class="picker-field">
		      <view>选择主题：{{ themes[selectedTheme] }}</view>
		    </picker>
		  </view>
		  
		  <view class="input-group">
		    <picker mode="selector" :range="publishMethods" v-model="selectedPublishMethod" class="picker-field">
		      <view>选择发布方式：{{ publishMethods[selectedPublishMethod] }}</view>
		    </picker>
		  </view>
		  
		  <button class="submit-button" @click="publish">发布</button>
		</view>
	</view>
		
</template>
  


<script>
export default {
  data() {
    return {
      imageSrc: '',
      price: '',
      description: '',
      themes: ['生活用品', '学习资料', '模玩周边', '户外运动'],
      selectedTheme: 0,
      publishMethods: ['在线出售', '面交'],
      selectedPublishMethod: 0,
    };
  },
  methods: {
    chooseImage() {
      uni.chooseImage({
        count: 1,
        success: (res) => {
          this.imageSrc = res.tempFilePaths[0];
        }
      });
    },
    publish() {
      // 在这里处理发布逻辑，如验证输入、发送数据到服务器等
      console.log('发布商品', this.price, this.description, this.themes[this.selectedTheme], this.publishMethods[this.selectedPublishMethod]);
      // 清空表单或给出提示等
    }
  }
}
</script>

<style lang="scss">
.publish-container {
  display: flex;
  flex-direction: column;
  padding: 20px;
  }
  .input-group, .upload-container {
    margin-bottom: 15px;
  }
  .input-field, .textarea-field, .picker-field, .upload-button, .submit-button {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 5px;
    border: 1px solid #ddd;
  }
  .textarea-field {
    height: 100px;
  }
  .upload-button, .submit-button {
    background-color: #007aff;
    color: white;
    border: none;
  }
  .uploaded-image {
    width: 100%;
    height: 200px;
    margin-top: 10px;
    object-fit: cover;
  }
  .all{
  	display: flex;
  	flex-direction: column;
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
  .label{
  	width: 100vw;
  	height: 10vh;
  	display: flex;
  	flex-direction: row;
  	justify-content: right;
  	align-items: center;
  	background-color: #F5F5F5;
  	.text1{
  		margin-left: 10px;
  		color: #9C9C9C;
  	}
  	.text{
  		margin-left: 10px;
  		font-size: 16px;
  	}
  	.text2{
  		margin-left: 10px;
  		margin-right: 15px;
  		font-size: 16px;
  	}
  }

</style>
