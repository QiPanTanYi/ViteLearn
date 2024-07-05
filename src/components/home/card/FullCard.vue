<template>
  <div class="wrapper">
    <!-- 使用v-for指令来循环渲染4个卡片 -->
    <div class="book" 
         v-for="(book, index) in books" 
         :key="index" 
         :class="{ 'book--expanded': expandedIndex === index }" 
         @click="toggleBook(index)"
         v-show="expandedIndex === index || !expandedIndex">
      <div class="book__cover">
        <div class="header-image">
          <div class="overlay"></div>
        </div>
        <div class="title-wrap">
          <h1 class="article-title">{{ book.title }}</h1>
        </div>
        <p class="book__cover-exerpt">
          {{ book.exerpt }}
          <!-- 社交图标可以在这里根据需要添加 -->
        </p>
      </div>
      <div class="book__content">
        <!-- 这里可以添加更多内容 -->
      </div>
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
      { title: 'Book 1', exerpt: 'Lorem ipsum dolor sit amet...', isExpanded: false },
      { title: 'Book 2', exerpt: 'Sed ut perspiciatis unde...', isExpanded: false },
      { title: 'Book 3', exerpt: 'At vero eos et accusamus...', isExpanded: false },
      { title: 'Book 4', exerpt: 'Nemo enim ipsam...', isExpanded: false }
    ]);

const expandedIndex = ref(null); // 当前展开的卡片索引
// 切换卡片状态的方法
// 切换卡片状态的方法
const toggleBook = index => {
       // 如果当前点击的卡片已经是展开状态，则关闭它，否则展开并隐藏其他卡片
       if (expandedIndex.value === index) {
        expandedIndex.value = null;
      } else {
        expandedIndex.value = index;
      }
    };

    // 将响应式数据和方法暴露给模板
    return {
      books,
      toggleBook,
      expandedIndex
    };
  }
};
</script>

<style>
.mr2 {
  margin-right: 1rem;
}
.ml2 {
  margin-left: 1rem;
}
.article-title {
  font-size: 2.5rem;
  line-height: 1;
 font-family: 'Roboto Condensed', sans-serif;
  text-align: center;
  letter-spacing: 0.025em;
  transition: font-size 0.45s ease-in-out, color 0.3s ease-out;
}
.header-image {
  height: 220px;
  background-image: url(@/assets/images/11.jpg);
  background-size: cover;
  background-position: center;
  margin-bottom: 3rem;
  position: relative;
  transition: all 0.45s ease-in-out;
}
.overlay {
  transition: all 0.3s ease-in-out;
  opacity: 0;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.title-wrap {
  transform: translateY(0);
  transition: transform 0.45s ease-in;
}
.drop-cap {
  font-size: 55px;
  line-height: 28px;
}
.wrapper {
  height: 100vh;
  display: flex;
  align-items: flex-start;
  justify-content: center;
}
.book__cover-exerpt {
  color: #6a6a6a;
  padding: 1rem 1.5rem;
  line-height: 1.6;
  text-align: center;
  opacity: 1;
  max-width: 370px;
  margin: 0 auto;
  display: block;
  transition: all 0.25s ease-in-out;
}
 
.book__cover {
  height: 100%;
  width: 100%;
}
.book__content {
  text-align: justify;
  word-wrap: break-word;
  font-size: 1.1rem;
  opacity: 0;
  transition: all 1.5s ease-in-out;
  max-width: 750px;
  margin: 0 auto 6rem;
  padding: 0 2rem;
}
.book__content p {
  line-height: 1.8;
  color: #3a3a3a;
  margin-bottom: 2.5rem;
}
.book {

  overflow: hidden;
  background: white;
  width: 240px;
	height: 340px;
  box-shadow: 0 20px 30px -10px #ccc;
  transition: all 0.5s ease-in-out;
  margin: 0 10px;
  margin-top: 20px;
}
.book:hover {
  box-shadow: 0 6px 50px 10px #cfcfcf;
}
.book--expanded {
  height: 100%;
  width: 100%;
  overflow-y: scroll;
}
.book--expanded .overlay {
  opacity: 0.95;
}
.book--expanded .article-title {
  color: white;
  font-size: 64px;
  letter-spacing: 0.05em;
}
.book--expanded .title-wrap {
  transform: translateY(-300px);
  color: white;
}
.book--expanded .book__cover-exerpt {
  opacity: 0;
}
.book--expanded .book__cover {
  height: 460px;
  margin-bottom: 6rem;
}
.book--expanded .book__content {
  opacity: 1;
}
.book--expanded .header-image {
  height: 100%;
}
span{
   margin-left: -35px;
}
span .fa {
   font-size: 17px;
   margin-left: 20px;
}

/* 添加的内容 */
.book__cover-expert {
  max-height: 10em;
}
.social {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all .5s ease-in-out;
}
.social i {
  margin: .5rem;
  color: #7a7a7a;
}
.book__expanded .book__content {
  opacity: 1;
}
.book__expanded .header-image {
  height: 40vw;
}
.book__expanded .book__cover {
  height: auto;
}
.book__expanded .book__cover-expert,
.book__expanded .social {
  opacity: 0;
  max-height: 0;
  padding: 0rem;
}

</style>