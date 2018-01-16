<template>
  <div id="app">
    <my-header></my-header>
    <my-nav></my-nav>
    <router-view class="main_content"></router-view>
    <my-footer></my-footer>
  </div>
</template>

<script>
import myHeader from './components/header'
import myFooter from './components/footer'
import myNav from './components/nav'

export default {
  name: 'app',
  components: {
    myHeader,
    myFooter,
    myNav
  }
}
</script>

<style>
body{
  margin: 0
}
a{
  text-decoration: none;
}
.main_content{
  position: relative;
  top:80px;
  width: 100%;
  margin-bottom: 135px;
  padding-left: 248px;
  box-sizing: border-box;
  overflow: hidden;
}
 @media screen and (max-width: 950px){
  .main_content {
     padding-left: 0;
  }
}
</style>
