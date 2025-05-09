<template>
  <view class="container">
    <!-- 统一导航栏 -->
	<view class="topbar">
		<view class="leftlabel">
			<view class="text1">购物车</view>
			<view class="text1">|</view>
			<view class="text">商品分类</view>
		</view>
		<view class="rightlabel">
			<view class="text1" @click="hdbjha">我</view>
			<view class="text1">|</view>
			<view class="text">消息</view>
			<view class="text1">|</view>
			<view class="text">收藏</view>
			<view class="text1">|</view>
			<view class="text">历史记录</view>
			<view class="text1">|</view>
			<view class="text">联系客服</view>
			<view class="text1">|</view>
			<view class="text" @click="jump">发布</view>
		</view>
	</view>
    <button @click="toggleSection" class="toggle-button">{{ buttonLabel }}</button>
    <view class="publish-container" v-if="isSectionVisible">
      <!-- 发布商品部分 -->
      <view class="upload-container">
        <!-- <button class="upload-button" @click="chooseImage">点击上传图片</button> -->
        <image class="uploaded-image" :src="imageSrc" v-if="imageSrc"></image>
		<u-upload
				:fileList="fileList1"
				@afterRead="afterRead"
				@delete="deletePic"
				name="1"
				multiple
				:maxCount="10"
				:previewFullImage="true"
			></u-upload>
      </view>
      <view class="input-group">
        <input type="text" v-model="price" placeholder="填写价格" class="input-field" />
      </view>
	  <view class="input-group">
	    <textarea v-model="type" placeholder="填写商品种类" class="textarea-field"></textarea>
	  </view>
      <view class="input-group">
        <textarea v-model="goods_name" placeholder="填写商品名称" class="textarea-field"></textarea>
      </view>
      <view class="input-group">
        <textarea v-model="description" placeholder="填写商品描述" class="textarea-field"></textarea>
      </view>
      <view class="input-group1">
        <picker mode="selector" :range="themes" v-model="divid_type" class="picker-field" @change="pickerChange1">
          <view class="picker-text">选择主题：{{ themes[divid_type] }}</view>
        </picker>
      </view>
      <view class="input-group1">
        <picker mode="selector" :range="publishMethods" v-model="selectedPublishMethod" class="picker-field" @change="pickerChange2">
          <view class="picker-text">选择发布方式：{{ publishMethods[selectedPublishMethod] }}</view>
        </picker>
      </view>
      <button class="submit-button" @click="publishData">发布</button>
    </view>
    <view v-if="!isSectionVisible">
      <!-- 发布帖子部分 -->
      <view class="upload-container">
<!--        <button class="upload-button" @click="chooseImage">点击上传图片</button>
        <image class="uploaded-image" :src="imageSrc" v-if="imageSrc"></image> -->
		<u-upload
				:fileList="fileList1"
				@afterRead="afterRead"
				@delete="deletePic"
				name="1"
				multiple
				:maxCount="10"
				:previewFullImage="true"
			></u-upload>
      </view>
      <view class="input-group">
        <textarea v-model="description" placeholder="填写帖子内容" class="textarea-field"></textarea>
      </view>
      <view class="input-group1">
        <picker mode="selector" :range="themes1" v-model="selectedTheme1" class="picker-field" @change="pickerChange">
          <view class="picker-text">选择主题：{{ themes1[selectedTheme1] }}</view>
        </picker>
      </view>
      <button class="submit-button" @click="publishData">发布</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      themes: ['生活用品', '学习资料', '模玩周边', '户外运动'],
      themes1: ['比赛组队', '分享日常', '评价吐槽', '兴趣爱好'],
      publishMethods: ['线上出售', '面交'],
      buttonLabel: '发布商品',
	  imageSrc: '',
	  price: '',
	  goods_name:'',
	  type:'',
	  description: '',
	  selectedPublishMethod: 0,
	  isSectionVisible: false ,// 初始化部分的显示状态为false，即隐藏
	  selectedTheme1: 0,
	  divid_type: 0,
	  base64:"",
	  fileList1: [],
    };
  },
  onLoad(option) { //option为object类型，会序列化上个页面传递的参数
  		// const a = JSON.parse(option.a)
  		// for (let i = 0; i < a.length; i++) {
  		//     // 访问每一项
  		//     this.user.push(a[i])
  		// }
		this.userid=option.a
		// this.username=option.b
  		console.log(this.userid)
  		// console.log(typeof this.goods)
  		},
  methods: {
    chooseImage() {
		let that = this
      uni.chooseImage({
        count: 1,
        success: (res) => {
          const file = res.tempFilePaths[0];
		  that.imageSrc = res.tempFilePaths[0]
		  // 创建一个 Canvas 元素
		  let canvas = document.createElement('canvas');
		  // 创建一个 Image 对象
		  let ctx = canvas.getContext('2d');
		  // 设置图片的 src 属性为本地图片路径
		  var img = new Image();
		  img.src = file;
		  img.onload = function() {
		    // 将图片绘制到 Canvas 上
		    canvas.width = img.width;
		    canvas.height = img.height;
		    ctx.drawImage(img, 0, 0);
		  
		    // 获取 Canvas 上的图片数据，并转换为 base64
		    that.base64 = canvas.toDataURL('image/jpeg');
		    // base64Data 包含了转换后的 base64 字符串
		    console.log('Base64 image data:',);
		  };
        }
      });
	  console.log(that.base64)
    },
    // base64(imageData) {
    //   uni.request({
    //     url: 'http://192.168.43.32:8000/search/test4',
    //     method: 'POST',
    //     data: {
    //        // Base64编码的图片数据
    //     },
    //     success: (res) => {
    //       console.log('上传成功', res.data);
    //     },
    //     fail: (error) => {
    //       console.error('上传失败', error);
    //     }
    //   });
    // },
    // publish() {
    //   console.log('发布商品', this.price, this.description, this.themes[this.divid_type], this.publishMethods[this.selectedPublishMethod]);
    // },
    toggleSection() {
      this.isSectionVisible = !this.isSectionVisible;
      this.buttonLabel = this.isSectionVisible ? '发布商品' : '发布帖子';
    },
    pickerChange(event) {
      const { value } = event.target;
      this.selectedTheme1 = value;
    },
    pickerChange1(event) {
      const { value } = event.target;
      this.divid_type = value;
    },
    pickerChange2(event) {
      const { value } = event.target;
      this.selectedPublishMethod = value;
    },
	
	    publishData() {
			
			let array=[];
			let that = this 
			for (let i = 1; i < that.fileList1.length; i++) {
			    array.push(that.fileList1[i].url);
			    console.log(array);
			}
			uni.request({
				url:'http://47.109.191.111：8000/addgoods/test4', // 后端接口地址
				// url:'http://47.109.191.111:8000/addgoods/test4',
				method:'POST',
				data: {
					goods_name: this.goods_name,
					short_description: this.description,
					price:this.price,
					image:this.base64,
					divid_type:this.divid_type,
					type:this.type,
					id:this.userid,
					name:this.username,
				},
					success: (res) => {
							console.log("请求成功", res);
							// that.error_message = res.data.error_message;
							// that.message = res.data.message
							// if(res.data.message==="登录成功！"){
							// 	setTimeout("alert('账号注册成功！')", 3000 )
							uni.navigateTo({
									url:'/pages/index/index'
								})
							// }
						},
					fail: (err) => {
						console.error("请求失败", err);
						},
			});
	},
	
	//         const response = await uni.request({
	//           url: 'http://172.23.161.32:8000/addgoods/test4', // 后端接口地址
	//           method: 'POST',
	//           data: {
	//             goods_name: this.goods_name,
	//             short_description: this.description,
	// 			price:this.price,
	// 			image:this.imageSrc,
	// 			divid_type:this.divid_type
	//           },
	//         });
	
	//         // 请求成功后的处理逻辑
	//         console.log('数据发布成功:', response.data);
	
	//         // 在这里可以进行其他操作，例如重定向到其他页面或者显示成功提示信息
	// 删除图片
		deletePic(event) {
			this[`fileList${event.name}`].splice(event.index, 1)
		},
		// 新增图片
		async afterRead(event) {
			// 当设置 multiple 为 true 时, file 为数组格式，否则为对象格式
			let lists = [].concat(event.file)
			let fileListLen = this[`fileList${event.name}`].length
			lists.map((item) => {
				this[`fileList${event.name}`].push({
					...item,
					status: 'uploading',
					message: '上传中'
				})
			})
			for (let i = 0; i < lists.length; i++) {
				const result = await this.uploadFilePromise(lists[i].url)
				let item = this[`fileList${event.name}`][fileListLen]
				this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
					status: 'success',
					message: '',
					url: result
				}))
				fileListLen++
			}
		},
		uploadFilePromise(url) {
			let array=[];
			let that = this 
			for (let i = 0; i < that.fileList1.length; i++) {
			    array.push(that.fileList1[i].url);
			    console.log(array);
			}
			array = JSON.stringify(array)
			console.log(array);
						return new Promise((resolve, reject) => {
							let a = uni.uploadFile({
								url: 'http://47.109.191.111:8000/addgoods/test4', // 仅为示例，非真实的接口地址
								filePath: array,
								name: 'file',
								filetype:Image,
								formData: {
									user: 'test'
								},
								success: (res) => {
									setTimeout(() => {
										resolve(res.data.data)
									}, 1000)
								}
							});
						})
					},

	}
  }

</script>

<style lang="scss">
.container{
	display: flex;
	flex-direction: column;
	padding: 20px;
}
.publish-container {
  display: flex;
  flex-direction: column;
  padding: 20px;
  }
  .input-group, .upload-container {
    margin-bottom: 15px;
  }
  .input-group1{
	  justify-content: center;
	  margin:auto;
	  margin-bottom: 15px;
  }
  .input-field, .textarea-field, .upload-button, .submit-button {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 5px;
    border: 1px solid #ddd;
  }
  .picker-field{
	width: 180px;
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
	display: grid;
	justify-content: center;
	margin:auto;
	width: 160px;
	height: 80px;
	font-size: 32px;
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


</style>

<!-- 剩余的问题就是如何把发布按钮居中 和如何改变upload的大小-->