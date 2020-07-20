<template>
  <div class="col-md-3 side-bar">
    <div class="panel panel-default corner-radius sidebar-resources">
      <div class="panel-heading text-center">
        <h3 class="panel-title">实战课程</h3>
      </div>
      <div class="panel-body">
        <Slider :slides="slides" v-slot="{ currentSlide }">
          <a :href="currentSlide.link" target="_blank">
            <img :alt="currentSlide.title" :title="currentSlide.title" :src="currentSlide.img" />
          </a>
        </Slider>
      </div>
    </div>
    <!-- 活跃用户 -->
    <div class="panel panel-default corner-radius panel-active-users">
      <div class="panel-heading text-center">
        <h3 class="panel-title">活跃用户</h3>
      </div>
      <div class="panel-body">
        <div class="users-label">
          <router-link
            v-for="(user, index) in activeUsers"
            :to="`/${user.name}`"
            :key="index"
            class="users-label-item"
          >
            <img :src="user.avatar" class="avatar-small inline-block" />
            {{ user.name }}
          </router-link>
        </div>
      </div>
    </div>
    <!-- 七天内最热 -->
    <div class="panel panel-default corner-radius panel-hot-topics">
      <div class="panel-heading text-center">
        <h3 class="panel-title">七天内最热</h3>
      </div>
      <div class="panel-body">
        <ul class="list">
          <li v-for="(article, index) in hotArticles" :key="index">
            <router-link :to="`/articles/${article.articleId}/content`">
              <span v-if="index === 0">🏆</span>
              <span v-else>{{ index + 1 }}.</span>
              {{ article.title }}
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheSidebar",
  data() {
    return {
      slides: [
        {
          title: "《Laravel 入门教程 - 从零到部署上线》",
          img:
            "https://cdn.learnku.com/uploads/banners/YpxKKNlSPdmwotO3u8An.jpg",
          link:
            "https://learnku.com/laravel/t/3383/laravel-the-first-chinese-new-book-laravel-tutorial"
        },
        {
          title: "《Laravel 进阶课程 - 从零构建论坛系统》",
          img:
            "https://cdn.learnku.com/uploads/banners/iNanVVOXdnYQ6jRfMdWE.png",
          link: "https://learnku.com/laravel/t/6592"
        },
        {
          title: "《Laravel 教程实战高级 - 构架 API 服务器》",
          img:
            "https://cdn.learnku.com/uploads/banners/tEd4GxhMp6VMh9e0hrUH.jpg",
          link: "https://learnku.com/laravel/t/7657"
        }
      ],
      activeUsers: [],
      hotArticles: [] // 最热文章
    };
  },
  created() {
    this.$axios.get("/users/active").then(response => {
      this.activeUsers = response.data;
    });

    // 通过 axios 执行 POST 请求来返回七天内最热文章，可以传递 num 来指定返回条数
    this.$axios.post("/articles/hot", { num: 10 }).then(response => {
      this.hotArticles = response.data;
    });
  }
};
</script>

<style scoped>
.carousel-inner img {
  display: block;
  margin: auto;
  line-height: 1;
  width: 70%;
  border: 1px solid #ddd;
  box-shadow: 0 0 10px #ccc;
  -moz-box-shadow: 0 0 10px #ccc;
  -webkit-box-shadow: 0 0 10px #ccc;
}
</style>