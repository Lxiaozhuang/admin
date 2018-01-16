<template>
    <div>
        <div class="inner">
           <div>
                <span>用户名:</span>
                <input type="text" v-model="user">
            </div>
            <div>
                <span>密码:</span>
                <input type="password" v-model="password">
            </div>
            
            <div class="info">
                <router-link to='cloud'>
                    <button @click="toSubmit">登录</button>
                </router-link>
                
            </div>
            <div class="headers">账号密码都是123456</div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            user:'',
            password:''
        }
    },
    methods:{
        toSubmit(){
            let data = {
                user: this.user,
                password:this.password
            }
            
            if(this.user==='123456' && this.password==='123456'){
                alert('登陆成功')
                window.localStorage.setItem('data',JSON.stringify(data));
            }
        }
    }
}
</script>

<style>
.inner{
    width: 500px;
    margin: 100px auto;
}
.headers{
    margin-top: 30px;
    font-size: 12px;
    text-align: center
}
.inner input{
    width: 400px;
    height: 40px;
    border-radius: 5px;
    margin-left: 10px;
    border: 1px solid #ccc
}
.inner input:focus{
    border: 1px solid rgb(35, 168, 230);
    outline: none
}
.inner span{
    display: inline-block;
    width: 60px;
    height: 60px;
    font: 16px/60px "微软雅黑";
    text-align: right;
    margin-right: 5px
}
.info{
    margin-top: 10px;
    text-align: center;
    
}
.inner button{
    width: 80px;
    height: 50px;
    font: 20px/50px "微软雅黑";
    background: rgb(11, 137, 221);
    color: #fff;
    text-align: center;
    border: none
}
.inner button:focus{
    outline: none
}
</style>
