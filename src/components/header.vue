<template>
  <header class="top-container">
      <div class="top-nav">
          <p>我们不一样</p>
      </div>
      <div v-if="contents" class="top-infor">
          <span>{{user.name}}欢迎您</span>
          <span>丨</span>
          <router-link to='cloud'>
              <button @click="tologout">注销</button>
          </router-link>
      </div>
      <div v-else class="top-infor">
          <router-link to="login">
          <button>登录</button>
          </router-link>
      </div>
  </header>
</template>

<script>
export default {
    data(){
        return {
            user:{
                name:'xiaozhuang'
            },
            contents:''
        }
    },
    methods:{
        tologin(){
            this.haslogin=true
        },
        tologout(){
            localStorage.clear()
            window.location.reload()
        }
    },
    beforeCreate(){
        if(localStorage.getItem("data")){
            this.contents=JSON.parse(localStorage.data)
        }
    }
}
</script>

<style>
    p{
        margin: 0
    }
    .top-container{
        position:fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 50px;
        font-size: 24px;
        box-shadow: 0 2px 5px 0 rgba(0,0,0,0.3);
        background: #fff;
        z-index: 100;
    }
    .top-nav{
        float: left;
        height: 50px;
        margin-left:30px;
        line-height: 50px;
        font-weight: bold;
        display:inline-block;
    }
    .top-infor{
        position: absolute;
        top:0;
        right: 50px;
        height: 50px;
        line-height: 50px;

    }
</style>
