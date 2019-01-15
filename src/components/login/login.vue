<template>
  <div>
    <div class="bg">
      <div class="login">
        <div class="title">JD-SHOP</div>
        <div class="text">后台管理系统</div>
        <el-input class="input" v-model="account" placeholder="请输入账号"></el-input>
        <el-input class="input" v-model="password" placeholder="请输入密码"></el-input>
        <el-button class="btn" type="primary" @click="toUser">登录</el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      account: "",
      password: ""
    };
  },
  methods: {
    toUser() {
      this.$router.push({ 'path': '/index' });
    }
  }
};
</script>

<style lang="scss" scoped>
@import "./login.scss";
</style>
