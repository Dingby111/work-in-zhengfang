<template>
  <view>
    <h1>历史浏览</h1>
    <uni-datetime-picker class="shijian" mode="date" @change="onDateChange" :value="currentDate"></uni-datetime-picker>
    <view id="items">
      <view v-for="(item, index) in paginatedItems" :key="index" class="item">
        <img :src="item.imgSrc" alt="商品图片" @click="goToItemDetail(item.id)">
        <view class="price">{{ item.price }}</view>
        <view class="description" @click="goToDescriptionPage(item.description)">{{ item.description }}</view>
        <view class="seller" >{{ item.seller }}</view> 
        <view class="time">{{ item.time_now }}</view> 
      </view>
    </view>
    <view class="pagination">
      <button @click="prevPage">上一页</button>
      <text>当前页：{{ currentPage }} / 总页数：{{ totalPages }}</text>
      <button @click="nextPage">下一页</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      itemsData: [
        {
          id: 1,
          imgSrc: "https://via.placeholder.com/200x150",
          price: "213元",
          description: "二手自行车，4成新",
          seller: "卖家：fucking boy",
          isSoldOut: true,
          browsingDate: ""  // 添加浏览日期属性
        },
      ],
      currentDate: new Date().toISOString().split('T')[0], // 默认为今天的日期
      currentPage: 1,
      pageSize: 8,
      totalItems: 0,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.itemsData.length / this.pageSize);
    },
    paginatedItems() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.itemsData.slice(start, end);
    }
  },
  methods: {
    onDateChange(event) {
      this.currentDate = event.target.value;
      this.goToItemDetailByDate(this.currentDate);
    },
    fetchItemsData(date) {
      const apiUrl = `/api/items?date=${date}`;
      fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
          this.itemsData = data.map(item => ({ ...item, browsingDate: date }));
          this.totalItems = data.length;
          this.currentPage = 1; // 重置为第一页
        })
        .catch(error => console.error('获取商品时出错：', error));
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
        this.$forceUpdate();
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
        this.$forceUpdate();
      }
    },
    goToItemDetailByDate(date) {
      // 根据选定的日期导航到商品详情页面
      uni.navigateTo({
        url: `/pages/itemDetail/itemDetail?date=${date}`
      });
    },
  },
  mounted() {
    this.fetchItemsData(this.currentDate); // 获取今天日期的初始数据
  }
};
</script>
<style>
.app-container {
  display: flex;
}

.sidebar {
  width: 20%;
  background-color: #f0f0f0;
  padding: 10px;
}

.content {
  width: 80%;
  padding: 10px;
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
		.posts {
		  display: flex;
		  flex-wrap: wrap;
		}
		
		.post {
		  width: 48%;
		  margin: 1%;
		  border: 1px solid #ddd;
		  border-radius: 5px;
		  overflow: hidden;
		}
		
		.post-image {
		  width: 100%;
		  height: 200px;
		}
		
		.post-info {
		  padding: 10px;
		}
		
		.post-title {
		  font-size: 16px;
		  font-weight: bold;
		  margin-bottom: 5px;
		}
		
		.post-description {
		  font-size: 14px;
		  color: #666;
		  margin-bottom: 10px;
		}
		
		.post-price {
		  font-size: 16px;
		  color: #e53e3e;
		}
		
		.year-item, .month-item {
		  margin-bottom: 10px;
		}
		
		.year-title, .month-title {
		  font-weight: bold;
		  cursor: pointer;
		}
		
		.months-list {
		  margin-left: 20px;
		}
		
		.days-list {
		  margin-left: 40px;
		}
		
		.day-item {
		  margin: 2px 0;
		}
		
		.pagination {
		  position: fixed; /* 固定位置 */
		  bottom: 0; /* 定位到视口的底部 */
		  left: 0; /* 定位到视口的左侧 */
		  width: 100%; /* 使分页栏宽度与视口宽度一致 */
		  background-color: white; /* 设置背景颜色以遮盖可能的内容重叠 */
		  box-shadow: 0 -2px 8px rgba(0,0,0,0.1); /* 添加阴影效果，提升视觉层次感 */
		  padding: 10px 0; /* 添加上下内边距 */
		  display: flex;
		  justify-content: center;
		  align-items: center;
		  z-index: 1000; /* 确保分页栏位于其他内容之上 */
		}


</style>
