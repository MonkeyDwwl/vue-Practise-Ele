<template lang="html">
  <header>
    <!-- 商家基本信息 -->
    <div class="seller">
      <img :src="seller.avatar" alt="">
      <div class="seler-info">
        <h2><i></i>{{seller.name}}</h2>
        <p class="delivery">{{seller.description}}/{{seller.deliveryTime}}分钟到达</p>
        <p class="pay"><i></i>{{seller.supports[0].description}}</p>
      </div>
      <div class="btn" @click="show=true">
        {{seller.supports.length}}个 >
      </div>
    </div>
    <!-- 公告 -->
    <div class="bulletin" @click="show=true">
      <i></i>
      <p>{{seller.bulletin}}</p>
      <em>></em>
    </div>
    <!-- 背景层 -->
    <div class="bg">
      <img :src="seller.avatar" alt="">
    </div>
    <!-- 弹出层 -->
    <transition name="bounce">
      <ele-popup :seller="seller" v-show="show" @close="show=false"></ele-popup>
    </transition>
  </header>
</template>

<script>
import Popup from '../Popup/Popup'
export default {
  data(){
    return{
      show : false,
    }
  },
  props:{
    seller : {
      type : Object,
      required : true
    }
  },
  components: {
    'ele-popup':Popup,
  }
};
</script>

<style lang="less" scoped>
@keyframes bounce-in {
  0%{transform: scale(0);}
  50%{transform: scale(1.5);}
  100%{transform: scale(1);}
}
@keyframes bounce-out {
  0%{transform: scale(1);}
  50%{transform: scale(1.5);}
  100%{transform: scale(0);}
}
.bounce-enter-active{animation: bounce-in .5s;}
.bounce-leave-active{animation: bounce-out .5s;}
header{
  position: relative;
  width: 100%;
  height: 134px;
  overflow: hidden;
  background:rgba(7,17, 27, .5);
  color: #fff;
  font-weight: 200;
  .seller{
    display: flex;
    margin: 24px 12px 18px 24px;
    img{
      width: 64px;
      height: 64px;
      margin-right: 16px;
      border-radius: 2px;
    }
    .seler-info{
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      h2{
        font-size: 16px;
        font-weight: bold;
        i{
          width: 30px;
          height: 18px;
          border-radius: 2px;
          background: url('./brand@2x.png') no-repeat;
          background-size: contain;
          display: inline-block;
          vertical-align: top;
          margin-right: 6px;
        }
      }
      .delivery{
        font-size: 12px;
      }
      .pay{
        font-size: 10px;
        i{
          width: 12px;
          height: 12px;
          background: url('./decrease_1@2x.png') no-repeat;
          display: inline-block;
          background-size: contain;
          vertical-align: top;
          margin-right: 4px;
        }
      }
    }
    .btn{
      font-size: 10px;
      width: 44px;
      height: 24px;
      line-height: 24px;
      background-color: rgba(0, 0, 0, .2);
      border-radius: 7px 8px;
      text-align: center;
      align-self: flex-end;
    }
  }
  .bg{
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    z-index: -1;
    img{
      width: 100%;
    }
    filter: blur(5px);
  }
  .bulletin{
    height: 28px;
    line-height: 28px;
    font-size: 10px;
    background: rgba(7, 17, 27, .2);
    display: flex;
    align-items: center;
    padding: 0 12px;
    i{
      min-width: 22px;
      min-height: 12px;
      display:block;
      background: url('./bulletin@2x.png') no-repeat;
      background-size: contain;
    }
    p{
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      margin:0 4px;
    }
  }
}
</style>
