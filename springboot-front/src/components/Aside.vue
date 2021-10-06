<template>
<div>
  <el-row class="tac">
    <el-col :span="12">

      <h5 style="color:green;font-size: 24px;left: 50px;">导航栏</h5>
      <el-menu
          active-text-color="#ffd04b"
          background-color="green"
          class="el-menu-vertical-demo"
          style="width:200px;height:650px"
          text-color="#fff">
<!--          default-active="user"-->
<!--          :default-openeds="[1]"-->
          <el-menu-item index="1">
            <i class="el-icon-location"></i>
            <span>信息管理</span>
          </el-menu-item>
<!--        <el-menu-item index="user" :route="{path:'/'}">用户管理-->
<!--        </el-menu-item>-->
          <el-menu-item index="2">
            <i class="el-icon-menu"></i>
            <span>功能菜单</span>
          </el-menu-item>
          <el-menu-item index="3">
            <i class="el-icon-document"></i>
            <span>使用文档</span>
          </el-menu-item>
          <el-menu-item index="4">
            <i class="el-icon-setting"></i>
            <span>应用设置</span>
          </el-menu-item>
      </el-menu>
    </el-col>
  </el-row>
</div>
</template>

<script>
export default {
  name: "Aside"
}
</script>

<style scoped>

</style>