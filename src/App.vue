<template>
  <div id="app">
    <ele-header :seller="seller"></ele-header>
    <ul class="nav">
      <li><router-link to="/">商品</router-link></li>
      <li><router-link to="/ratings">评论</router-link></li>
      <li><router-link to="/seller">商家</router-link></li>
    </ul>
    <router-view></router-view>
  </div>
</template>

<script>
//引入子组件
import Header from './components/Header/Header'
//引入json格式的数据
const shop = require('./api/data.json');
export default {
  name: 'app',
  data(){
    return{
      seller : {} //商家信息,初始值为空
    }
  },
  created(){
    //do something after creating vue instance
    this.seller = shop.seller;
  },
  components:{
    "ele-header":Header //注册Header组件
  }
}
</script>

<style lang="less">
.nav{
  display: flex;
  justify-content: space-around;
  height: 40px;
  line-height: 40px;
  border:1px solid rgba(7, 17, 27, .2);
  a{
    color: rgb(77, 85, 93);
    font-size: 14px;
    text-decoration: none;
    &.router-link-exact-active{
      color: rgb(240, 20, 20);
    }
  }
}
</style>
