<template>
  <div id="index">
    <mt-header title="人员出行登记系统" fixed></mt-header>
    <div class="content-div">
      <mt-field label="用户名" placeholder="请输入用户名" v-model="username"></mt-field>
      <mt-field label="密码" placeholder="请输入密码" type="password" v-model="password"></mt-field>
      <br>
      <mt-button type="primary" size="large" @click.native="handleClick">登陆</mt-button>
      <a class="register-btn" @click="toReg">去注册</a>
    </div>
    <footer-div></footer-div>
  </div>
</template>
<script>
import * as sso from '@/api/auth'
import FooterDiv from "../components/FooterDiv.vue";
import { Toast } from "mint-ui";
export default {
  components: {
    "footer-div": FooterDiv
  },
  data() {
    return {
      username: "",
      password: ""
    };
  },
  methods: {
    async handleClick() {
      await sso.login({
        username: this.username,
        password: this.password
      }).then((res)=>{
        if(res.data.isRight==true){
          localStorage.setItem('uinfo', JSON.stringify(res.data));
          this.$router.push('/');
        }else{
          Toast("账号或密码错误！");
        }
      });
    },

    toReg() {
      this.$router.push('/register')
    }
  }
};
</script>
<style scoped>
/* #index {
} */
.content-div {
  margin: 90px 45px;
}
.text-header {
  margin-top: 10px;
  margin-left: 5px;
  font-size: 18px;
  line-height: 40px;
  border-bottom: 1px solid #cccccc;
}
li {
  margin-left: 10px;
  margin-top: 10px;
}
span {
  border-radius: 8px;
  background-color: #cccccc;
  margin-right: 8px;
  display: inline-block;
  padding: 5px;
  font-size: 12px;
}
.register-btn{
  color: #26a2ff;
  float: right;
  margin-top: 4px;
}
</style>