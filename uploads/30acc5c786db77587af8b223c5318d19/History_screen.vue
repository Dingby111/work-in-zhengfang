<template>
  <view>
   <!-- 日期选择器 -->
    <view class="date-picker-container">
       <uni-datetime-picker mode="date" @change="onDateChange" :value="currentDate" />
    </view>
  <view class="container">
    <view class="title">购物历史记录</view>
    <view class="content">
      <view class="time-list">
        <view 
          class="time-item" 
          v-for="(item, index) in historyList" 
          :key="`time-${index}`"
          @click="selectItem(index)"
        >
          {{ item.time }}
        </view>
      </view>
      <view class="history-list" v-if="selectedItem">
        <view class="history-item">
          <img class="item-image" :src="selectedItem.imgUrl">
          <view class="item-info">
            <view class="item-name">{{ selectedItem.name }}</view>
            <view class="item-time">{{ selectedItem.time }}</view>
          </view>
        </view>
      </view>
    </view>
  </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      historyList: [
        { name: '商品A', time: '2023-04-01', imgUrl: 'https://example.com/product_a.jpg' },
        { name: '商品B', time: '2023-04-02', imgUrl: 'https://example.com/product_b.jpg' },
        
      ],
      selectedItem: null,
	  currentDate: '2024-04-07',
    }
  },
  methods: {
    selectItem(index) {
      this.selectedItem = this.historyList[index];
    },
	onDateChange(e) {
	      this.currentDate = e.detail.value;
	      console.log('选择的日期是：', this.currentDate);
	      // 在这里，你可以添加更多的处理逻辑，比如根据选择的日期过滤你的收藏列表
	    },
  }
}
</script>

<style scoped>
.container {
  padding: 20px;
}

.title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 20px;
}

.content {
  display: flex;
}

.time-list {
  flex: 0 1 200px; 
  display: flex;
  flex-direction: column;
  align-items: flex-start; 
  padding-right: 20px; 
  cursor: pointer; 
}

.history-list {
  flex: 1; 
  display: flex;
  flex-direction: column;
}

.history-item, .time-item {
  display: flex;
  align-items: center; 
  padding: 10px 0;
}

.item-image {
  width: 60px; 
  height: 60px; 
  margin-right: 10px; 
}

.item-info {
  display: flex;
  flex-direction: column;
}

.item-name, .item-time {
  font-size: 16px;
}

.item-time {
  color: #999;
}

.date-picker-container {
  position: absolute;
  left: 0;
  top: 0;
  padding: 20px;
  /* 根据需要调整样式 */
}
</style>
onsubmit(res){
			console.log(res)
			this.search = 
			let that=this
			uni.request({
				url:
				method:'POST',
				data:that.search,
				success: (res) => {
					console.log("请求成功",res);
					that.result=res;
					let string1=this.result.data.Match
					uni.navigateTo({
						url:
					})
				},
				fail: (err)	=>{
					console.error("请求失败",err)
				},
				
			});
		}