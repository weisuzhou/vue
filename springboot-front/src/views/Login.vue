<template>
<!--  <div style="width: 100%; height: 100vh; overflow: hidden;"> &lt;!&ndash;  :style="bg" 加背景图片&ndash;&gt;-->
   <div :style="imgSrc">
    <div style="width: 400px; margin: 100px auto">
      <div style="font-size: 30px; text-align: center; padding: 30px 0">欢迎登录</div>
      <el-form ref="form" :model="form" size="normal" :rules="rules">
        <el-form-item prop="username">
          <el-input prefix-icon="el-icon-user-solid" v-model="form.username" placeholder="请输入账号"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input prefix-icon="el-icon-lock" v-model="form.password" show-password placeholder="请输入密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-radio v-model="form.role" :label="1">管理员</el-radio>
          <el-radio v-model="form.role" :label="2">普通用户</el-radio>
        </el-form-item>
        <el-form-item>
          <el-button style="width: 100%" type="primary" @click="login">登 录</el-button>
        </el-form-item>
        <el-form-item><el-button type="text" @click="$router.push('/register')">前往注册 >> </el-button></el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import request from "../utils/request";


export default {
  name: "Login",
  components: {
  },
  data() {
    return {
      form: {},
      rules: {
        username: [
          {required: true, message: '请输入用户名', trigger: 'blur'},
        ],
        password: [
          {required: true, message: '请输入密码', trigger: 'blur'},
        ],
      },
      validCode: '',
      // 加背景图片
       imgSrc: {
         backgroundImage: "url(" + require("../assets/R-C.jpg") + ")",
         backgroundRepeat: "no-repeat",
         width:"100%",
         height:"100%",
         position:"fixed",
         margin:"0px",
         backgroundSize:"100%,100%"
       }
    }
  },
  created(){
    sessionStorage.removeItem("user")
  },
  methods: {
    login()
    {
      this.$refs['form'].validate((valid)=>{
        if(valid){
          request.post("/api/user/login", this.form).then(res => {
            if (res.code === '0') {
              this.$message({
                type: "success",
                message: "登录成功"
              })
              this.$router.push("/")  //登录成功之后进行页面的跳转，跳转到主页
            }
            else
            {
              this.$message({
                type: "error",
                message: res.msg
              })
            }
          })
        }
      })

    }
}
}
</script>

<style scoped>

</style>