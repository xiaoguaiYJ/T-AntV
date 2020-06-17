<template>
  <div class="login-container">
    <div class="login-weaper  animated bounceInDown">
      <a-card class="login-left">
        <div class="login-time">
          {{ date }}
        </div>
        <div style="text-align: center">
          <h1>Ant Design Vue Pro</h1>
          <h3>基于Ant Design Vue构建</h3>
          <h3>By <a href="https://github.com/TyCoding/cloud-template">TyCoding</a></h3>
        </div>
      </a-card>
      <a-card class="login-right">
        <a-form-model
          ref="ruleForm"
          :model="form"
          :rules="rules"
          class="login-form"
        >

          <div class="title-container">
            <h3 class="title">Login</h3>
          </div>

          <a-form-model-item ref="username" prop="username">
            <a-input
              v-model="form.username"
              size="large"
              type="text"
            >
              <a-icon slot="prefix" type="user" />
            </a-input>
          </a-form-model-item>

          <a-form-model-item ref="password" prop="password">
            <a-input-password
              v-model="form.password"
              size="large"
              type="text"
            >
              <a-icon slot="prefix" type="lock" />
            </a-input-password>
          </a-form-model-item>

          <a-button
            :loading="loading"
            type="primary"
            style="width:100%;margin-bottom:30px;"
            @click.stop.prevent="handleLogin"
          >Login
          </a-button>
        </a-form-model>
      </a-card>
    </div>
  </div>
</template>

<script>
import { parseTime } from '@/utils/index'

export default {
  name: 'Login',
  components: {},
  data() {
    return {
      date: parseTime(new Date().getTime(), ''),
      form: {
        username: 'admin',
        password: 'admin'
      },
      rules: {
        username: [{ required: true, message: 'Please input Username', trigger: 'blur' }],
        password: [{ required: true, message: 'Please input Password', trigger: 'blur' }]
      },
      capsTooltip: false,
      loading: false,
      showDialog: false,
      redirect: undefined,
      otherQuery: {}
    }
  },
  watch: {
    $route: {
      handler: function(route) {
        const query = route.query
        if (query) {
          this.redirect = query.redirect
          this.otherQuery = this.getOtherQuery(query)
        }
      },
      immediate: true
    }
  },
  mounted() {
    const _this = this
    this.timer = setInterval(() => {
      _this.date = parseTime(new Date().getTime(), '')
    }, 1000)
  },
  beforeDestroy() {
    if (this.timer) {
      clearInterval(this.timer)
    }
  },
  methods: {
    handleLogin() {
      this.$refs.ruleForm.validate(valid => {
        if (valid) {
          this.$store.dispatch('user/login', this.form)
            .then(() => {
              this.$router.push({ path: this.redirect || '/', query: this.otherQuery })
              this.loading = false
            })
            .catch(() => {
              this.loading = false
            })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    getOtherQuery(query) {
      return Object.keys(query).reduce((acc, cur) => {
        if (cur !== 'redirect') {
          acc[cur] = query[cur]
        }
        return acc
      }, {})
    }

  }
}
</script>
<style lang="less" scoped>
  @bg: #2d3a4b;
  @dark_gray: #889aa4;
  @light_gray: #eee;
  @-webkit-keyframes animate-cloud {
    0% {
      background-position: 600px 100%
    }
    to {
      background-position: 0 100%
    }
  }

  .ant-card-bordered {
    border: none !important;
  }

  .login-container {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    position: relative;
    width: 100%;
    height: 100%;
    margin: 0 auto;
    background: url(../../assets/bg_cloud.jpg) 0 bottom repeat-x #049ec4;
    -webkit-animation: animate-cloud 20s linear infinite;
    animation: animate-cloud 20s linear infinite;

    .login-weaper {
      margin: 0 auto;
      width: 1000px;
      -webkit-box-shadow: -4px 5px 10px rgba(0, 0, 0, .4);
      box-shadow: -4px 5px 10px rgba(0, 0, 0, .4);
    }

    .bounceInDown {
      -webkit-animation-name: bounceInDown;
      animation-name: bounceInDown;
    }

    .animated {
      -webkit-animation-duration: 1s;
      animation-duration: 1s;
      -webkit-animation-fill-mode: both;
      animation-fill-mode: both;
    }

    .login-time {
      position: absolute;
      left: 25px;
      top: 25px;
      width: 100%;
      color: #fff !important;
      font-weight: 400;
      opacity: .9;
      font-size: 20px;
      overflow: hidden;
    }

    h1, h2, h3 {
      color: #fff !important;
    }

    .login-left {
      border-top-left-radius: 5px;
      border-bottom-left-radius: 5px;
      -webkit-box-pack: center;
      -ms-flex-pack: center;
      justify-content: center;
      -webkit-box-orient: vertical;
      -webkit-box-direction: normal;
      -ms-flex-direction: column;
      flex-direction: column;
      background-color: #409eff;
      color: #fff !important;
      float: left;
      width: 50%;
      position: relative;
      min-height: 500px;
      -webkit-box-align: center;
      -ms-flex-align: center;
      align-items: center;
      display: -webkit-box;
      display: -ms-flexbox;
      display: flex;
    }

    .login-right {
      -webkit-box-sizing: border-box;
      box-sizing: border-box;
      border-left: none;
      border-top-right-radius: 5px;
      border-bottom-right-radius: 5px;
      color: #fff;
      background-color: #fff;
      width: 50%;
      float: left;
      min-height: 500px;
    }

    .login-form {
      position: relative;
      max-width: 100%;
      margin: 0 auto;
      overflow: hidden;
      padding: 0 56px;
    }

    .svg-container {
      position: absolute;
      top: -5px;
      font-size: 14px;
      color: @dark_gray;
      cursor: pointer;
      user-select: none;
      padding: 6px 5px 6px 15px;
      vertical-align: middle;
      width: 30px;
      display: inline-block;
    }

    .el-input {
      position: initial !important;
    }

    .title-container {
      position: relative;

      .title {
        font-size: 26px;
        color: #606266 !important;
        margin: 50px auto 40px auto;
        text-align: center;
        font-weight: bold;
      }
    }

    .el-icon-user::before {
      content: "\e6e3";
    }

    .show-pwd {
      position: absolute;
      right: 33px;
      top: 0px;
      font-size: 16px;
      color: @dark_gray;
      cursor: pointer;
      user-select: none;
    }

    @media screen and (max-width: 992px) {
      .login-left {
        display: none;
      }

      .login-right {
        width: 100%;
      }
    }
  }

</style>
