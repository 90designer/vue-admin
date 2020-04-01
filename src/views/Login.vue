<template>
  <div id="login">
    <el-page-header @back="goBack" content="详情页面"></el-page-header>
    <div class="block">
      <el-carousel height="150px">
        <el-carousel-item v-for="item in 4" :key="item">
          <h3 class="small">{{ item }}</h3>
          <img src="../assets/banner.png" />
        </el-carousel-item>
      </el-carousel>
    </div>
  </div>
</template>
<script>
export default {
  name: "login",
  data() {
    return {};
  },
  methods: {
    formatTooltip(val) {
      return val / 100;
    },
    goBack() {
      alert("返回");
    }
  }
};
</script>
<!--scoped 当前文件有效-->
<style lang="scss" scoped>
#login {
  // vh 可是区域的百分比
  height: 100vh;
  background-color: #fcfcfc;
}
.el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 150px;
  margin: 0;
}
</style>
