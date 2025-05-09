<template>
  <div class="app-container">
    <div class="sidebar">
      <div class="years-list">
        <div v-for="year in years" :key="year.year" class="year-item">
          <div class="year-title" @click="toggleYear(year.year)">
            {{ year.year }}
          </div>
          <div v-if="year.showMonths" class="months-list">
            <div v-for="month in year.months" :key="month.month" class="month-item">
              <div class="month-title" @click.stop="toggleMonth(year.year, month.month)">
                {{ month.month }}月
              </div>
              <div v-if="month.showDays" class="days-list">
                <div v-for="day in month.days" :key="day" class="day-item" @dblclick="onDayDblClick(year.year, month.month, day)">
                  {{ day }}日
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="posts">
        <div class="post" v-for="item in items" :key="item.id">
          <img class="post-image" :src="item.image" alt="商品图片">
          <div class="post-info">
            <div class="post-title">{{ item.title }}</div>
            <div class="post-description">{{ item.description }}</div>
            <div class="post-price">￥{{ item.price }}</div>
          </div>
        </div>
      </div>
      <div class="pagination">
        <button @click="prevPage">上一页</button>
        <div>{{ currentPage }}/{{ totalPages }}</div>
        <button @click="nextPage">下一页</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      years: [
        {
          year: 2023,
          showMonths: false,
          months: [
            { month: 1, showDays: false, days: [1, 2, 3, 4, 5] },
            // 更多月份和日期...
          ],
        },
        // 更多年份...
      ],
      items: [
        { id: 1, title: '商品1', description: '商品描述1', price: 100, image: '商品1的图片URL' },
        { id: 2, title: '商品2', description: '商品描述2', price: 200, image: '商品2的图片URL' },
        // 更多商品信息...
      ],
      currentPage: 1,
      totalPages: 5,
    };
  },
  methods: {
    toggleYear(year) {
      const yearObj = this.years.find(y => y.year === year);
      if (yearObj) {
        yearObj.showMonths = !yearObj.showMonths;
      }
    },
    toggleMonth(year, month) {
      const yearObj = this.years.find(y => y.year === year);
      if (yearObj) {
        const monthObj = yearObj.months.find(m => m.month === month);
        if (monthObj) {
          monthObj.showDays = !monthObj.showDays;
        }
      }
    },
    prevPage() {
      if (this.currentPage > 1) this.currentPage--;
    },
    nextPage() {
      if (this.currentPage < this.totalPages) this.currentPage++;
    },
    onDayDblClick(year, month, day) {
      const url = `/date/${year}/${month}/${day}`;
      window.location.href = url;
    },
				
  },
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
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
</style>
