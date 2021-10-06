<template>
<div style="height: 50px;line-height: 50px;border-bottom: 1px solid #ccc;display:flex">
  <div style="width: 200px;padding-left: 0px;font-size:24px;font-weight: bold;color:dodgerblue">新生入学登记系统</div>
  <div style="flex:1"></div>
  <div style="width: 100px">
    <el-dropdown>
    <span class="el-dropdown-link">
      用户身份<i class="el-icon-arrow-down el-icon--right"></i>
    </span>
      <template #dropdown>
        <el-dropdown-menu>
          <el-dropdown-item>admin</el-dropdown-item>
          <el-dropdown-item @click="$router.push('/login')">退出系统</el-dropdown-item>

        </el-dropdown-menu>
      </template>
    </el-dropdown>


  </div>


</div>
</template>

<script>
export default {
  name: "Header"
}
</script>

<style scoped>

</style>