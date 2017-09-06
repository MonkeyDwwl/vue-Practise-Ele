<template>
  <div id="buy">
    <transition name="rotate">
      <div class="sub" v-show="food.count" @click.stop="deleteFromCart">
        <i class="iconfont icon-jian"></i>
      </div>
    </transition>

    <transition name="fade">
      <div class="count" v-show="food.count">{{food.count}}</div>
    </transition>

    <div class="add" @click.stop="addToCart">
      <i class="iconfont icon-jia"></i>
    </div>
  </div>
</template>
<script>
export default {
  name: "buy",
  props:{
    food : {
      type : Object,
      required : true
    }
  },
  methods:{
    //添加购物车
    addToCart(){
      if(this.food.count){
        this.food.count++;
      }else{
        this.$set(this.food,'count',1);
      }
    },
    deleteFromCart(){
      if(this.food.count){
        this.food.count--;
      }
    },
  }
}
</script>
<style lang="less" scoped>
@import "../../assets/css/font.css";
// 过渡样式
.rotate-enter,.rotate-leave-active{transform: translateX(200%) rotateZ(360deg);}
.rotate-enter-active,.rotate-leave-active{transition: all .5s;}
.fade-enter,.fade-leave-active{transform: translateX(200%) rotateZ(360deg);}
.fade-enter-active,.fade-leave-active{transition: all .5s;}

#buy{
  width: 72px;
  height: 24px;
  position: relative;
  .sub,.add{
    width: 24px;
    height: 24px;
    color: rgb(0,160,220);
    position: absolute;
    top: 0;
    i{
      font-size: 24px;
    }
  }
  .sub{
    left:0;
    top: -2px;
  }
  .add{
    right: 0;
  }
  .count{
    text-align: center;
    line-height: 24px;
  }
}
</style>
