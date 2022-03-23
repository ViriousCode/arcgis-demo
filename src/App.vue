<template>
  <el-menu :default-active="activeIndex2" class="el-menu-demo" mode="horizontal" @select="handleSelect"
    background-color="#545c64" text-color="#fff" active-text-color="#ffd04b" :router="true">
    <el-menu-item index="1">首页</el-menu-item>
    <el-sub-menu index="2">
      <template #title>我的工作台</template>
      <el-menu-item index="/">ToDoList</el-menu-item>
      <el-menu-item index="/about">About</el-menu-item>
      <el-menu-item index="2-3">选项3</el-menu-item>
      <el-sub-menu index="2-4">
        <template #title>选项4</template>
        <el-menu-item index="2-4-1">选项1</el-menu-item>
        <el-menu-item index="2-4-2">选项2</el-menu-item>
        <el-menu-item index="2-4-3">选项3</el-menu-item>
      </el-sub-menu>
    </el-sub-menu>
    <el-menu-item index="3" disabled>消息中心</el-menu-item>
    <el-menu-item index="4">订单管理</el-menu-item>
  </el-menu>
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div> -->
  <router-view />
</template>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
</style>