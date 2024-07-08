<template>
  <div class="container" @click="deselectAll">
		<div
      v-for="number in numbers"
      :key="number"
      class="card"
      :class="{ fullscreen: selectedCard === number }"
      @click="selectCard(number)"
    >
      <!-- 卡片内容 -->
      {{ number }}
    </div>
	</div>
</template>

<script setup>
import { ref } from 'vue';
const numbers = ref([1, 2, 3, 4, 5]);
const selectedCard = ref(null); // 用于跟踪被点击的卡片


const selectCard = (cardNumber) => {
  if (selectedCard.value === cardNumber) {
    selectedCard.value = null; // 如果点击的卡片已经是选中状态，则取消选中
  } else {
    selectedCard.value = cardNumber; // 否则，选中这个卡片
  }
};

</script>

<style scoped>
.container{
	max-width: 1000px;
	position: relative;
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
	transform-style: preserve-3d;
	cursor: pointer; /* 添加鼠标手势 */
}
.container .card{
	position: relative;
	width: 180px;
	height: 240px;
	background: #fff;
	margin: 0 10px;
	display: flex;
	justify-content: center;
	align-items: center;
	border-radius: 4px;
	box-shadow: 0 5px 15px rgba(0,0,0,.1);
	transition: 0.5s;
	overflow: hidden;
	transform-style: preserve-3d;
	cursor: pointer; /* 添加鼠标手势 */
}
.container:hover .card{
	transform: perspective(500px) rotateY(30deg);
}
.container .card:hover{
	transform: perspective(500px) rotateY(0deg);
}
.container .card:hover ~ .card{
	transform: perspective(500px) rotateY(-30deg);
}
/* 选中的卡片样式 */
.card.selected {
  z-index: 10;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 0;
  margin: 0;
  box-shadow: none;
  background: #fff; /* 根据需要调整背景 */
}

/* 点击容器时，取消所有卡片的选中状态 */
.container:active .card {
  transform: scale(0.8);
  opacity: 0.3;
}
</style>
