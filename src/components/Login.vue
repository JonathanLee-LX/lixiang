<template>
    <div class="container">
        <div class="head">
          <div class="brand">
          </div>
          <h1>印象笔记</h1>
        </div>
        <div class="body">
          <form action="/login" method="POST" id="login">
            <div class="email-wrapper">
              <input type="email" name="email" placeholder="用户名或者邮箱" v-model="email"><br>
              <div class="error-info" v-show="email_error"><span>请确认邮箱地址是否有效！</span></div>
            </div>
            <div class="psw-wrapper" v-show="showPsw">
              <input type="password" name="password" placeholder="输入密码" v-model="psw"><br>
              <div class="error-info" v-show="psw_error"><span>请确认密码或邮箱是否正确！</span></div>
            </div>
            <div class="option-wrapper">
              <input type="checkbox" name="remember" v-model="isRemember"><label for="remember">30天内记住我</label><br>
            </div>
            <div class="sub-wrapper">
              <button type="submit" name="sub-btn" @click.prevent="login">登录</button><br>
            </div>
          </form>
           <div class="footer">
            <a href="/forget">忘记密码？</a>
            <ul class="help-info">
                 <li>预设邮箱：<strong>123456@qq.com</strong></li>
                 <li>预设密码：<strong>123456</strong></li>
             </ul>
            </div>
        </div>
        <div class="register">
            <span>没有账号？</span><br>
            <a href="/register">创建账户</a>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import qs from "qs";
import router from "../router/index";

export default {
  name: "Login",
  data() {
    return {
      email: "",
      psw: "",
      isRemember: false,
      showPsw: false,
      email_error: false,
      psw_error: false
    };
  },
  methods: {
    login() {
      if (!this.email) {
        this.email_error = true;
        setTimeout(() => {
          this.email_error = false;
        }, 3000);
        return;
      }
      if (!this.psw) {
        this.showPsw = true;
        return;
      }

     var vm = this;
      axios
        .post("http://localhost:3000/login", qs.stringify({
            email: this.email,
            psw: this.psw,
            isRemember: this.isRemember
         }))
        .then(function(response) {
         router.push("/success");
        })
        .catch(function(error) {
          vm.psw_error = true;
          setTimeout(() => {
            vm.psw_error = false;
          }, 3000);
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a{
    text-decoration: none;
    color: #42b983;
}
.container {
  margin: 100px auto;
  width: 40%;
  min-width: 400px;
  height: 100%;
}
.head {
  width: 100%;
}
.body {
  background-color: #fff;
  padding: 30px;
  box-shadow: 1px 1px 3px #ccc;
}
.email-wrapper {
  margin-bottom: 10px;
}
.email-wrapper input {
  width: 100%;
  height: 2em;
  text-indent: 10px;
  border-radius: 5px;
  font-size: 20px;
  border: 1px solid #ccc;
}
.psw-wrapper {
  margin-bottom: 10px;
}
.psw-wrapper input {
  width: 100%;
  height: 2em;
  text-indent: 10px;
  border-radius: 5px;
  font-size: 20px;
  border: 1px solid #ccc;
}
.option-wrapper {
  margin-bottom: 10px;
  text-align: left;
}
.sub-wrapper {
  margin-bottom: 10px;
}
.sub-wrapper button {
  width: 100%;
  height: 2em;
  font-size: 20px;
  color: #fff;
  background-color: #42b983;
  border: 1px solid #fff;
  border-radius: 5px;
}
.sub-wrapper button:hover {
  background-color: #3ba374;
}
.error-info {
  color: brown;
  font-size: 0.7em;
  text-align: left;
}
.help-info{
    list-style: none;
}
.help-info li{
    float: left;
    margin-right: 10px;
    font-size: 0.6em;
}
.register{
    margin-top: 20px;
}
</style>

