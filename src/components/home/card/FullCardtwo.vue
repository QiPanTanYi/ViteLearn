<template>
  <div class="wrapper flex flex-col items-center justify-center h-screen">
    <!-- 使用v-for指令来循环渲染4个卡片 -->
    <div class="book relative" v-for="(book, index) in books" :key="index"
         :class="{ 'book--expanded': book.isExpanded }" @click="() => toggleBook(index)">
      <div class="book__cover">
        <div class="header-image">
          <!-- 覆盖层 -->
          <div class="overlay absolute inset-0 transition-opacity z-10"></div>
        </div>
        <div class="title-wrap">
          <h1 class="article-title text-center">{{ book.title }}</h1>
        </div>
        <p class="book__cover-exerpt text-center">{{ book.exerpt }}</p>
      </div>
      <div class="book__content text-justify leading-relaxed">
        <!-- 这里可以添加更多内容 -->
      </div>
      <!-- 遮罩层，用于实现全屏点击退出 -->
      <div v-if="book.isExpanded" class="backdrop fixed inset-0 z-0 bg-black opacity-50 cursor-pointer" @click="() => toggleBook(index)"></div>
    </div>
  </div>
</template>

<script>
 import { ref } from 'vue';
// import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
// import { library } from '@fortawesome/fontawesome-svg-core';
// import { faFacebook, faTwitter, faLinkedin, faInstagram } from '@fortawesome/free-brands-svg-icons';

// library.add(faFacebook, faTwitter, faLinkedin, faInstagram);

export default {
  setup() {
    // 使用ref创建响应式数据
    const books = ref([
      { title: 'Dark House', exerpt: 'Lorem ipsum dolor sit amet...', isExpanded: false },
      { title: 'Book 2', exerpt: 'Sed ut perspiciatis unde...', isExpanded: false },
      { title: 'Book 3', exerpt: 'At vero eos et accusamus...', isExpanded: false },
      { title: 'Book 4', exerpt: 'Nemo enim ipsam...', isExpanded: false }
    ]);

    // 使用computed计算属性来处理isExpanded状态
    const isExpanded = computed(() => books.value.map(book => book.isExpanded));
// 切换卡片状态的方法
const toggleBook = index => {
      books.value[index].isExpanded = !books.value[index].isExpanded;
    };

    // 将响应式数据和方法暴露给模板
    return {
      books,
      toggleBook
    };
  }
};
</script>
<style lang="css" scoped>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>