<template>
	<h1>我的收藏</h1>
	    <view id="items">
	        <!-- 商品项 -->
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">213元</view>
	                <view class="description">二手自行车，4成新</view>
	                <view class="seller">卖家：fucking boy</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">70.5元</view>
	                <view class="description">二手行李箱</view>
	                <view class="seller">卖家：Qiao ba</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">10.2元</view>
	                <view class="description">二手书籍，整套</view>
	                <view class="seller">卖家：Tian giegie</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">421元</view>
	                <view class="description">亚斯娜手办</view>
	                <view class="seller">卖家：巴乔的匿名男友</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <!-- 更多商品项 -->
	        <!-- 请根据需要复制以上商品项结构并修改相应信息 -->
	    </view>
	
	
	    <view id="items">
	        <!-- 商品项 -->
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">230元</view>
	                <view class="description">二手索尼相机</view>
	                <view class="seller">卖家：巴乔的匿名男友</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">15元</view>
	                <view class="description">二手打印机</view>
	                <view class="seller">卖家：Qiao ba</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">138元</view>
	                <view class="description">二手翡翠利达</view>
	                <view class="seller">卖家：巴乔的匿名男友</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <view class="item">
	            <img src="https://via.placeholder.com/200x150" alt="商品1">
	            <view class="item-info">
	                <view class="price">11.5元</view>
	                <view class="description">精美的手工艺品</view>
	                <view class="seller">卖家：John Doe</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        </view>
	        <!-- 更多商品项 -->
	        <!-- 请根据需要复制以上商品项结构并修改相应信息 -->
	    </view>
	
	    <ul class="pagination">
	        <li class="disabled">上一页</li>
	        <li class="active" data-page="1">1</li>
	        <li data-page="2">2</li>
	        <li data-page="3">3</li>
	        <li class="disabled">...</li>
	        <li data-page="7">7</li>
	        <li data-page="next">下一页</li>
	        <li data-page="last">末页</li>
	    </ul>
</template>

<script>
	function toggleFavorite(button) {
	            button.classList.toggle('favorited');
	            button.classList.contains('favorited')
	            button.textContent = '取消收藏';
	
	        }
	
	        document.addEventListener('DOMContentLoaded', function () {
	            const pagination = document.querySelector('.pagination');
	            pagination.addEventListener('click', function (e) {
	                if (e.target.tagName === 'LI' && !e.target.classList.contains('disabled')) {
	                    // 移除当前激活的分页按钮的激活状态
	                    document.querySelector('.pagination li.active').classList.remove('active');
	                    // 设置被点击的分页按钮为激活状态
	                    e.target.classList.add('active');
	                    // 获取被点击的分页按钮的页码
	                    const page = e.target.getAttribute('data-page');
	                    // 根据页码更新页面内容
	                    updatePageContent(page);
	                }
	            });
	        });
	
	        function updatePageContent(page) {
	            // 这里是一个示例函数，用于模拟更新页面内容
	            // 在实际应用中，你需要根据页码从服务器获取数据，并更新页面内容
	            console.log(`更新页面内容到第 ${page} 页`);
	        }
	
	        const itemsData = [
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
	        ];
	        function renderItems(items) {
	            const itemsContainer = document.getElementById('items');
	            itemsContainer.innerHTML = ''; // 清空现有内容
	
	            items.forEach(item => {
	                const itemElement = document.createElement('view');
	                itemElement.classList.add('item');
	
	                itemElement.innerHTML = `
	            <img src="${item.imgSrc}" alt="商品图片">
	            <view class="item-info">
	                <view class="price">${item.price}</view>
	                <view class="description">${item.description}</view>
	                <view class="seller">${item.seller}</view>
	            </view>
	            <button class="favorite-btn" onclick="toggleFavorite(this)">取消收藏</button>
	        `;
	
	                itemsContainer.appendChild(itemElement);
	            });
	        }
	
	        // 在页面加载完成后渲染商品项
	        document.addEventListener('DOMContentLoaded', function () {
	            renderItems(itemsData);
	        });
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
</style>
