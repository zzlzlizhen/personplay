<template>
    <div class="login_container">
        <div class="login_box">
            <!--头像区域-->
            <div class="avatar_box">
                <img src="../assets/logo.png"/>
            </div>
            <!-- 登陆表单区域 -->
            <el-form ref="loginFormRef" :model="userEntity" :rules="loginFormRules" label-width="0" class="login_form">
                <el-form-item prop="username">
                    <el-input v-model="userEntity.username"></el-input>
                </el-form-item>
                 <el-form-item prop="pwd">
                    <el-input v-model="userEntity.pwd"></el-input>
                </el-form-item>
                <el-form-item class="butts" >
                    <el-button type="primary" @click="login">确定</el-button>
                    <el-button type="info" @click="restLoginForm">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>
<script>
export default {
  data () {
    return {
      userEntity: {
        userId: '',
        username: 'admin',
        pwd: '123456',
        token: ''
      },
      // 表单验证规则
      loginFormRules: {
        username: [
          { required: true, message: '请输入登陆用户名', trigge: true },
          { min: 3, max: 20, message: '用户名长度在3~20个字符', trigge: true }
        ],
        pwd: [
          { required: true, message: '请输入登陆密码', trigge: true },
          { min: 3, max: 20, message: '密码的长度在3~20个字符', trigge: true }
        ]
      }
    }
  },
  methods: {
    login () {
      this.$refs.loginFormRef.validate(async valid => {
        // console.log(valid)
        if (!valid) {
          return false
        }
        const { data: res } = await this.$http.post('http://localhost:8087/user/login', this.userEntity)
        console.log(res)
      })
    },
    // 点击重置按钮，重置登陆表单
    restLoginForm () {
    //   console.log(this)
      this.$refs.loginFormRef.resetFields()
    }
  }
}
</script>
<style lang="less" scoped>
.login_container {
    background-color: #2b4b6b;
    height: 100%;
}
.login_box{
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 3px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%)
}
.avatar_box{
    width: 130px;
    width: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    box-shadow: 0 0 10px #ddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%,-50%);
    background-color: #fff;
    padding: 10px;
    img{
        width: 100%;
        height: 100%;
        border-radius: 50%;
        background-color:#eee;
    }
}
.butts{
        display: flex;
        justify-content: flex-end;
}
.login_form{
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
}

</style>
