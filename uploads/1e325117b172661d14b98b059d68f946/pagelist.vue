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
		<!-- 标签分类块 -->
		<view class="label">
			<view class="text">生活用品</view>
			<view class="text1">|</view>
			<view class="text">学习资料</view>
			<view class="text1">|</view>
			<view class="text">模玩周边</view>
			<view class="text1">|</view>
			<view class="text2">户外运动</view>
		</view>
		<!-- 商品详情界面 -->
<!-- 		<view class="detail">
			<view v-for="(item, index) in itemsData" :key="index" class="item">
			  <img :src="item.imgSrc" :alt="item.alt" class="itemimg">
			  <view class="item-info">
				<view class="price">{{ item.price }}</view>
				<view class="description">{{ item.description }}</view>
				<view class="seller">{{ item.seller }}</view>
			  </view>
			</view>
		</view> -->
		<view class="detail">
			<view v-for="(item, index) in goods" :key="index" class="item">
			  <img src="https://via.placeholder.com/200x150"  class="itemimg">
			  <view class="item-info">
				<view class="seller">{{ item.fields.goods_name }}</view>
				<view class="description">{{ item.fields.short_description }}</view>
				<view class="price">{{ item.fields.price }}</view>
			  </view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				itemsData:[
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "213元",
								description: "二手自行车，4成新",
								seller: "卖家：fucking boy"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "70.5元",
								description: "二手行李箱",
								seller: "卖家：Qiao ba"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "10.2元",
								description: "二手书籍，整套",
								seller: "卖家：Tian giegie"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "421元",
								description: "亚丝娜手办",
								seller: "卖家：巴乔的匿名男友"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "15元",
								description: "二手打印机",
								seller: "卖家：Qiao ba"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "138元",
								description: "二手翡翠利达",
								seller: "卖家：巴乔的匿名男友"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "11.5元",
								description: "精美的手工艺品套",
								seller: "卖家：John Doe"
							},
							{
								imgSrc: "https://via.placeholder.com/200x150",
								price: "230元",
								description: "二手索尼相机套",
								seller: "卖家：巴乔的匿名男友"
							},
				  	 // 更多商品数据...
				],
				goods:[],
			}
		},
		onLoad(option) { //option为object类型，会序列化上个页面传递的参数
				const a = JSON.parse(option.a)
				for (let i = 0; i < a.length; i++) {
				    // 访问每一项
				    this.goods.push(a[i])
				}
				console.log(this.goods)
				console.log(typeof this.goods)
				},
		methods: {
			
		}
	}
</script>

<style lang="scss">
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
	.detail{
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-around; /* 更合理的分布 */
		padding: 20px;
		gap: 20px; /* 为每个项目添加间隙 */
		.items {
		    display: flex;
		    flex-wrap: wrap;
		    justify-content: space-around; /* 更合理的分布 */
		    padding: 20px;
		    gap: 20px; /* 为每个项目添加间隙 */
			.itemimg{
				width: 100%; /* 图片宽度调整为100%，以自适应容器宽度 */
				height: 150px;
				object-fit: cover;
				border-top-left-radius: 12px;
				border-top-right-radius: 12px;
			}
			.item-info {
			    padding: 10px;
			    display: flex;
			    flex-direction: column;
			    justify-content: space-between;
			}
			.price {
			    color: #007bff;
			    font-size: 16px; /* 调整字体大小 */
			    font-weight: bold;
			}
			
			.description {
			    color: #333;
			    font-size: 14px;
			    margin: 5px 0;
			    overflow: hidden;
			    text-overflow: ellipsis;
			    white-space: nowrap;
			}
			
			.seller {
			    color: #666;
			    font-size: 12px;
			}
		}
		.item:hover {
		    transform: translateY(-5px);
		}
	}
</style>
