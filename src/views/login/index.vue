<template>
  <div class="login-container">
    <div class="bg-container"></div>
    <div class="left-container">
      <div class="title">精选保险 就在微服{{ name }}</div>
      <div class="name">北京微服保险经纪有限公司</div>
    </div>
    <el-form ref="loginForm" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on"
      label-position="left">
      <div class="title-container">
        <!-- <h1 class="name">北京微服保险经纪有限公司</h1> -->
        <h3 class="title">保险核心业务系统</h3>
      </div>

      <el-form-item prop="username">
        <span class="svg-container svg-container_login">
          <svg-icon icon-class="user" /></span>
        <el-input class="loginField" name="username" type="text" v-model="loginForm.username" autoComplete="on"
          :autofocus="true" placeholder="请输入用户名" />
      </el-form-item>

      <el-form-item prop="password">
        <span class="svg-container"> <svg-icon icon-class="password" /></span>
        <el-input name="password" :type="passwordType" @keyup.enter.native="handleLogin" v-model="loginForm.password"
          autoComplete="on" placeholder="请输入密码" />
        <span class="show-pwd" title="显示密码" @click="showPwd">
          <svg-icon icon-class="eye" /></span>
      </el-form-item>
      <el-button size="large" type="primary" class="sqPrimary" style="
          width: 100%;
          margin-bottom: 30px;
          background-color: #f5a30e;
          border-color: #f5a30e;
          line-height: 2;
        " :loading="loading" @click.native.prevent="handleLogin">
        登 录
      </el-button>
    </el-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import { storeToRefs } from 'pinia'
import { useUserStore } from '@/store/modules/user'

export default defineComponent({
  setup() {
    const userStore = useUserStore()
    const loginForm = reactive({
      username: 'admin',
      password: 'admin',
    })
    const loginRules = reactive({
      username: [
        { required: true, trigger: 'blur,change', message: '请输入用户名' },
      ],
      password: [
        { required: true, trigger: 'blur,change', message: '请输入密码' },
      ],
    })
    const passwordType = ref('password')
    const loading = ref(false)
    const handleLogin = () => {
      console.log('登录')
      userStore.login(loginForm)
    }
    const showPwd = () => {
      if (passwordType.value === 'password') {
        passwordType.value = ''
      } else {
        passwordType.value = 'password'
      }
    }
    return {
      loginForm,
      loginRules,
      passwordType,
      loading,
      handleLogin,
      showPwd,
    }
  },
})
</script>
<style lang="scss">
$bg: #2d3a4b;
$inputBG: #766e68;
$light_gray: #eee;

/* reset element-ui css */
.login-container {
  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;

    input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;

      &:-webkit-autofill {
        box-shadow: 0 0 0px 1000px $inputBG inset !important;
        -webkit-text-fill-color: #fff !important;
      }
    }
  }

  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.34);
    border-radius: 5px;
    color: #454545;
  }
}
</style>

<style lang="scss" scoped>
$bg: #2d3a4b;
$dark_gray: #889aa4;
$light_gray: #eee;

.login-container {
  position: fixed;
  height: 100%;
  width: 100%;
  background-color: #95c2cf;
  // background: url('../../assets/images/loginBG.jpg') no-repeat center center;
  background-size: cover;
  // background-color: $bg;
  overflow: auto;

  .bg-container {
    position: absolute;
    left: 250px;
    right: 0;
    top: 28%;
    width: 549px;
    height: 220px;

    background: url("../../assets/images/bg.jpg") no-repeat;
    background-size: contain;
  }

  .left-container {
    position: absolute;
    left: 0;
    right: 0;
    top: 60%;
    width: 549px;
    height: 220px;
    color: #fff;

    .title {
      padding-left: 180px;
      margin-top: -40px;
      font-size: 42px;
      text-align: left;
      margin-bottom: 20px;
      font-weight: bold;
    }

    .name {
      padding-left: 180px;
      font-size: 18px;
      text-align: left;
    }
  }

  .login-form {
    position: absolute;
    left: 0;
    right: 0;
    top: 50%;
    transform: translate(90%, -55%);
    width: 334px;
    padding: 35px 35px 15px 35px;
    margin: 20px auto;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.4);

    .svg-container_login {
      font-size: 14px;
    }
  }

  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: #fff;
    vertical-align: middle;
    width: 30px;
    display: inline-block;

    &_login {
      font-size: 20px;
    }
  }

  .title-container {
    position: relative;

    .name {
      color: #000;
      font-size: 18px;
      margin-bottom: 10px;
      text-align: center;
    }

    .title {
      font-size: 25px;
      font-weight: 400;
      color: #555;
      margin: 0px auto 10px auto;
      text-align: center;
      font-weight: bold;
      width: 200px;
      height: 50px;
      // text-indent: -9999em;
      // background: url("../../assets/images/loginLOGO.png") no-repeat center;
    }

    .set-language {
      color: #fff;
      position: absolute;
      top: 5px;
      right: 0px;
    }
  }

  .show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: #fff;
    cursor: pointer;
    user-select: none;
  }

  .thirdparty-button {
    position: absolute;
    right: 35px;
    bottom: 28px;
  }
}
</style>
