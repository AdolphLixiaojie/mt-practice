<template>
  <div id="app">
    <!-- header -->
    <app-header :poiInfo="poiInfo"></app-header>
    <!-- nav -->
    <app-nav :commentNum="commentNum"></app-nav>

    <router-view />
  </div>
</template>

<script>
import Header from "./components/header/Header";
import Nav from "./components/nav/Nav";
export default {
  name: "App",
  data() {
    return {
      poiInfo: {},
      commentNum: 0,
    };
  },
  components: {
    "app-header": Header,
    "app-nav": Nav,
  },
  created() {
    //  fetch获取数据
    fetch("/api/goods")
      .then((res) => {
        return res.json();
      })
      .then((response) => {
        // console.log(response)
        if (response.code == 0) {
          this.poiInfo = response.data.poi_info;
          // console.log(this.poiInfo);
        }
      });
    fetch("/api/ratings")
      .then((res) => {
        return res.json();
      })
      .then((response) => {
        if (response.code == 0) {
          this.commentNum = response.data.comment_num;
        }
      });
  },
};
</script>

<style>
/* 全局引入从图标 */
@import url(./common/css/icon.css);
</style>
