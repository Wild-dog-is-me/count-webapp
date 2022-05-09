<template>
  <div class="header">
    <img :src="'./static/images/logo.png'">
    <div class="title">我的记账系统</div>
    <div class="user"><i class="el-icon-user-solid"></i>admin </div>
  </div>
</template>

<script>
  export default {
    name: "headerTop"
  }
</script>

<style scoped>
  .header {
    width: 100%;
    height: 60px;
    line-height: 60px;
    background-color: cornflowerblue;
    text-align: left;
    display: flex;
  }

  .header img {
    width: 42px;
    margin: 9px;
  }

  .header .title{
    font-size: 18px;
    color: white;
    font-weight: bolder;
    width: calc(100% - 145px);
  }

  .header .user{
    cursor: pointer;
    font-size: 14px;
    color: white;
    font-weight: bolder;
  }
</style>
