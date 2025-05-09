<template>
	<view class="all">
		<h1>我的收藏</h1>
		<view id="items" v-if="totalPages > 0">
			<view v-for="(item, index) in visibleItems" :key="index" class="item">
			  <img :src="item.imgSrc" :alt="item.alt">
			  <view class="item-info">
				<view class="price">{{ item.price }}</view>
				<view class="description">{{ item.description }}</view>
				<view class="seller">{{ item.seller }}</view>
			  </view>
			  <button class="favorite-btn" @click="toggleFavorite(item)">取消收藏</button>
			</view>
		</view>
		<view v-else>
		      <text>No content available.</text>
		</view>
      <view class="pagination">
        <button v-for="page in totalPages" :key="page" :class="{ active: currentPage === page }" @tap="changePage(page)">
          {{ page }}
        </button>
      </view>
	</view>
</template>

<script>
export default {
  data() {
    return {
		itemsPerPage: 8, // 每页显示的项数
		currentPage: 1 ,// 当前页码
      itemsData: [
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
      ]
    };
  },
    computed: {
      totalPages() {
        return Math.ceil(this.itemsData.length / this.itemsPerPage);
      },
      visibleItems() {
        const start = (this.currentPage - 1) * this.itemsPerPage;
        const end = start + this.itemsPerPage;
        return this.itemsData.slice(start, end);
      }
    },
  mounted() {
	for (let i = 1; i <= 20; i++) {
	      this.itemsData.push(`Item ${i}`);
	    }
  },
  methods: {
	changePage(page) {
	      this.currentPage = page;
	    },
	  
  }
};
</script>

<style>
	body {
		     font-family: Arial, sans-serif;
		     margin: 0;
		     padding: 0;
		     background-color: #f4f4f4;
		 }
		 
		 h1 {
		     text-align: center;
		     color: #333;
		     margin: 20px;
		 }
		 
		 #items {
		     display: flex;
		     flex-wrap: wrap;
		     justify-content: space-around; /* 更合理的分布 */
		     padding: 20px;
		     gap: 20px; /* 为每个项目添加间隙 */
		 }
		 
		 .item:hover {
		     transform: translateY(-5px);
		 }
		 
		 .item img {
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
		 
		 .favorite-btn, .favorite-btn.favorited {
		     background-color: #007bff;
		     border: none;
		     padding: 8px 16px; /* 调整按钮内边距 */
		     color: white;
		     cursor: pointer;
		     font-weight: bold;
		     position: absolute;
		     bottom: 10px; /* 调整按钮位置 */
		     left: 50%;
		     transform: translateX(-50%);
		 }
		 
		 .favorite-btn.favorited {
		     background-color: #28a745;
		 }
		 
		 .pagination {
		     display: flex;
		     list-style: none;
		     padding: 0;
		     position: fixed;
		     bottom: 20px;
		     left: 50%;
		     transform: translateX(-50%);
		 }
		 
		 .pagination li {
		     margin: 0 5px;
		     border: 1px solid #ddd;
		     padding: 5px 10px;
		     cursor: pointer;
		 }
		 
		 .pagination li.active {
		     background-color: #007bff;
		     color: #ffffff;
		     border-color: #007bff;
		 }
		 
		 .pagination li.disabled {
		     color: #cccccc;
		     cursor: not-allowed;
		 }
		 
		 .item {
		     background-color: white;
		     border-radius: 10px;
		     box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		     transition: transform 0.3s ease;
		     width: calc(100% / 4 - 40px); /* 适应4列布局 */
		     position: relative;
		     padding-bottom: 60px; /* 调整底部填充 */
		 }
		 .favorite-btn, .favorite-btn.favorited {
		     background-color: #007bff;
		     border: none;
		     padding: 6px 12px; /* 减小内边距 */
		     color: white;
		     cursor: pointer;
		     font-weight: bold;
		     font-size: 12px; /* 减小字体大小 */
		     position: absolute;
		     bottom: 10px;
		     left: 50%;
		     transform: translateX(-50%);
		 }
		.pagination {
		  margin-top: 20px;
		  display: flex;
		  justify-content: center;
		}
		.pagination button {
		  margin: 0 5px;
		  cursor: pointer;
		  background-color: #007bff;
		  color: white;
		  border: none;
		  border-radius: 5px;
		  transition: background-color 0.3s ease;
		}
		.pagination button:hover {
		  background-color: #0056b3;
		}
		.pagination button.active {
		  background-color: #0056b3;
		}
</style>
