<template>
  <div>
      <div v-if="uesrinfo" id="myactivetime">
        模拟数据，祝你学习愉快
      </div>
      <div v-if="!uesrinfo" class="prompt">
          只有QQ号登陆才能查看信息
      </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      contents:'',
      uesrinfo:false
    }
  },
  beforeCreate(){
    
    if(localStorage.getItem("data")){
      this.uesrinfo=true
      this.contents=JSON.parse(localStorage.data)
      console.log(this.contents)
    }
  }
}
</script>

<style>
#myactivetime {
    position: relative;
    left: 50%;
    width: 90%;
    height: 600px;
    margin-left: -45%;
    box-shadow: 0 0 10px #EDE68A;
    border-radius: 10px;
    text-align: center
  } 
  .prompt {
    position: relative;
    left: 50%;
    width: 400px;
    height: 40px;
    margin-left: -200px;
    box-shadow: 0 0 6px #BF382A;
    border-radius: 8px;
    line-height: 40px;
    text-align: center;
  }
  @media screen and (max-width: 420px) {
    .prompt {
      width: 310px;
      margin-left: -155px;
      font-size: 15px;
    }
  }
</style>
