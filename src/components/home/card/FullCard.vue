<template>
   <div :class="['wrapper', { 'wrapper--expanded': isWrapperExpanded }]">
    <!-- 使用v-for指令来循环渲染4个卡片 -->
    <div class="book" 
         v-for="(book, index) in books" 
         :key="index" 
         :class="{ 'book--expanded': expandedIndex === index }" 
         @click="toggleBook(index)"
         v-show="expandedIndex === index || showAllCards">

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
         <p>
          <span class="drop-cap">O</span>Lorem ipsum dolor sit amet,
          consectetur adipisicing elit. Molestias est incidunt odit ea
          adipisci animi nihil voluptates iure beatae explicabo asperiores
          enim ex placeat itaque minus error temporibus voluptate corporis
          suscipit commodi voluptatibus praesentium molestiae, perspiciatis
          nulla. Accusantium harum nisi maiores, velit perferendis, nesciunt
          ad, porro sequi aliquid maxime molestias!
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab nobis
          fuga delectus tempore. Odio ipsa voluptate ex nobis ratione
          consequatur dignissimos dolorum culpa, ipsam sit dolorem itaque
          excepturi, natus sed deleniti incidunt ipsum asperiores! Molestiae
          cumque quam nulla, nam inventore. Necessitatibus blanditiis cumque
          laboriosam, id, ad unde quo ipsum nulla.
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Earum
          accusantium velit expedita, minima sapiente unde magnam dicta.
          Consequuntur cumque numquam sed deserunt, quidem officia illo
          blanditiis ipsum, commodi distinctio quam molestias dolore,
          doloremque corporis? Rem ad recusandae delectus accusamus, harum
          quisquam perferendis dolor aut consectetur nesciunt atque laborum ab
          dolores.
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad, neque,
          magnam. Impedit deleniti ad alias, unde vero quis mollitia, tenetur
          minima porro, officia iusto quae harum labore nostrum aliquid aut
          maxime, architecto in reprehenderit. Doloribus pariatur quam fuga
          sed modi veniam, vel corporis magnam quis eius cumque voluptate,
          dolore repellendus labore nobis, voluptatibus dicta sapiente
          doloremque! Enim dicta totam debitis cumque similique, natus,
          consequatur quidem cum incidunt, sint quos. Ea.
        </p>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Provident
          voluptatum possimus dolores nesciunt natus quaerat quas quo quam
          obcaecati ducimus totam quia sint, et nobis nisi tenetur id
          aspernatur quibusdam molestiae reprehenderit sed incidunt. Voluptas
          error necessitatibus sed inventore, quasi facilis, est. Asperiores
          atque laboriosam inventore quis eos nulla. Fuga neque odit maiores
          facilis voluptas nemo numquam, eos amet molestias.
        </p>
      </div>
    </div>
 </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const books = ref([
  { title: 'Book 1', exerpt: 'Lorem ipsum dolor sit amet...', isExpanded: false },
  { title: 'Book 2', exerpt: 'Sed ut perspiciatis unde...', isExpanded: false },
  { title: 'Book 3', exerpt: 'At vero eos et accusamus...', isExpanded: false },
  { title: 'Book 4', exerpt: 'Nemo enim ipsam...', isExpanded: false }
]);
const expandedIndex = ref(null); // 当前展开的卡片索引
const showAllCards = ref(true); // 控制是否显示所有卡片

// 使用计算属性决定是否添加 'wrapper--expanded' 类
const isWrapperExpanded = computed(() => expandedIndex.value !== null);
const wrapperClasses = computed(() => ['wrapper', isWrapperExpanded.value ? 'wrapper--expanded' : '']);

const toggleBook = index => {
  if (expandedIndex.value === index) {
    expandedIndex.value = null;
    showAllCards.value = true;
  } else {
    expandedIndex.value = index;
    showAllCards.value = false;
  }
};

// 无需返回，因为 script setup 会自动暴露所有顶级的响应式引用和函数
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
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
}
.wrapper--expanded {
  z-index: 1000; /* 或者你想要的任何 z-index 值 */
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
  margin-top: 250px;
}
.book:hover {
  box-shadow: 0 6px 50px 10px #cfcfcf;
}
.book--expanded {
  height: 100%;
  width: 100%;
  overflow-y: scroll;
  z-index: 100;
  margin: 0;
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
html.no-scroll,
body.no-scroll {
  overflow: hidden;
}
</style>