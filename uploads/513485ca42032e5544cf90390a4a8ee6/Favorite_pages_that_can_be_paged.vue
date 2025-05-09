<template>
  <view>
    <h1>我的收藏</h1>
    <view id="items">
      <view v-for="(item, index) in paginatedItems" :key="item.id" class="item">
        <img :src="item.imgSrc" alt="商品图片">
        <view class="item-info">
          <view class="price">{{ item.price }}</view>
          <view class="description">{{ item.description }}</view>
          <view class="seller">{{ item.seller }}</view>
        </view>
        <button class="favorite-btn" @tap="removeItem(item.id)">取消收藏</button>
      </view>
    </view>
    <view class="pagination">
          <button @tap="prevPage">上一页</button>
          <text>当前页：{{ currentPage }} / 总页数：{{ totalPages }}</text>
          <button @tap="nextPage">下一页</button>
        </view>
  </view>
</template>



<script>
	export default {
	  data() {
	    return {
	      itemsData: [
	        // 商品数据...
	        {
	          id: 1,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "213元",
	          description: "二手自行车，4成新",
	          seller: "卖家：fucking boy"
	        },
	        {
	          id: 2,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	        {
	          id: 3,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	        {
	          id: 4,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	        {
	          id: 5,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	        {
	          id: 6,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	        {
	          id: 7,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	        {
	          id: 8,
	          imgSrc: "https://via.placeholder.com/200x150",
	          price: "70.5元",
	          description: "二手行李箱",
	          seller: "卖家：Qiao ba"
	        },
	      ],
	      currentPage: 1,
	      pageSize: 8,
	      totalItems: 0,
	    };
	  },
	  computed: {
	      totalPages() {
	        return Math.ceil(this.totalItems / this.pageSize);
	      },
	      paginatedItems() {
	        const start = (this.currentPage - 1) * this.pageSize;
	        const end = start + this.pageSize;
	        return this.itemsData.slice(start, end);
	      }
	  },
	  methods: {
	    removeItem(itemId) {
	      this.itemsData = this.itemsData.filter(item => item.id !== itemId);
	      // 在uni-app中，可能需要手动通知视图更新
	      this.$forceUpdate();
	    },
	    nextPage() {
	          if (this.currentPage < this.totalPages) {
	            this.currentPage++;
	          }
	        },
	        prevPage() {
	          if (this.currentPage > 1) {
	            this.currentPage--;
	          }
	        }
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
	/* 你的样式代码 */
</style>
