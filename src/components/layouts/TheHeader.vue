<template>
  <div class="navbar navbar-default topnav">
    <div class="container">
      <div class="navbar-header">
        <router-link to="/" class="logo">
          gi
          <i class="fa fa-book fa-lg">BLOG</i>
        </router-link>
        <button type="button" class="navbar-toggle" @click="toggleNav">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
      </div>

      <div
        id="top-navbar-collapse"
        :class="['collapse', 'navbar-collapse', { in: showCollapsedNav }]"
      >
        <!-- 入口组件 -->

        <div class="navbar-right">
          <SearchInput />
          <TheEntry />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// 引入 TheEntry.vue 的默认值
import TheEntry from "@/components/layouts/TheEntry";
// 引入 SearchInput.vue 默认值
import SearchInput from "@/components/layouts/SearchInput";
export default {
  name: "TheHeader",
  components: {
    TheEntry,
    // 注册 SearchInput
    SearchInput
  },
  data() {
    return {
      activeNavIndex: 0,
      showCollapsedNav: false
    };
  },

  methods: {
    changeNavIndex(index) {
      this.activeNavIndex = index;
    },
    toggleNav() {
      this.showCollapsedNav = !this.showCollapsedNav;
    }
  }
};
</script>

<style scoped>
.title {
  display: none;
}
.navbar-default .navbar-nav > .active > a {
  background: rgba(0, 0, 0, 0.03);
}
.navbar-header .logo {
  margin-top: 8px;
  margin-bottom: 8px;
  height: 34px;
  line-height: 34px;
  display: inline-block;
  min-width: 70px;
}
</style>