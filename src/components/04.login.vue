<template>
     <div>
        <div class="section">
            <div class="location">
                <span>当前位置：</span>
                <a href="/index.html">首页</a> &gt;
                <a href="/login.html">会员登录</a>
            </div>
        </div>
        <div class="section">
            <div class="wrapper">
                <div class="bg-wrap">
                    <div class="nav-tit">
                        <a class="selected" href="javascript:;">账户登录</a>
                        <i>|</i>
                        <a href="/register.html">免费注册</a>
                    </div>

                    <div id="loginform" name="loginform" class="login-box">
                        <div class="input-box">
                            <input id="txtUserName" v-model="userName" name="txtUserName" type="text" placeholder="用户名/手机/邮箱" maxlength="50">
                        </div>
                        <div class="input-box">
                            <input id="txtPassword" v-model="userPass" name="txtPassword" type="password" placeholder="输入登录密码" maxlength="16">
                        </div>
                        <div class="btn-box">
                            <input id="btnSubmit" name="btnSubmit" type="submit" @click="login" value="立即登录">
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    name:'login',
    data:function(){
        return {
            userName:'',
            userPass:''
        }
    },

  //方法
  methods:{
      login(){
          //获取用户名
          //获取密码
          //提交
          this.$axios.post('site/account/login',{
              user_name:this.userName,
              password:this.userPass
          }).then(response=>{
              console.log(response)
              if(response.data.status==0){
                  //用户提示
                  this.$Notice.success({
                      title:'提示',
                      desc:response.data.message
                  });
                  //vuex修改
                  this.$store.commit('changeLogin',true);
                  //返回上一页
                  this.$router.go(-1);
              }else if(response.data.status==1){ 
                  //用户提示
                  this.$Notice.error({
                      title:'提示',
                       desc:response.data.message
                  });
                  
              }
          })
      }
  }
}
</script>
<style>

</style>

