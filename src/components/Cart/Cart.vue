<template>
  <div>
    <div id="cart" @click="toggleList">
      <div class="cart-left">
        <div class="cart-outer">
          <div class="cart-inner" :class="{active:count}">
            <i class="iconfont icon-gouwuche"></i>
          </div>
          <div class="count" v-show="count">{{count}}</div>
        </div>
      </div>
      <div class="cart-md">
        <strong>¥{{total}}</strong>
        <span>另需配送费¥{{this.deliveryPrice}}</span>
      </div>
      <div class="cart-right" :class="{active:total>=this.minPrice}">
        {{payDesc}}
      </div>
    </div>
    <!-- 购物车列表 -->
    <div class="cart-list" v-show = "show">
      <div class="cart-list-hd">
        <h2>购物车</h2>
        <span @click="clear">清空</span>
      </div>
      <div class="cart-list-bd">
        <ul>
          <li v-for="(food,index) in cartGoods">
            <h3>{{food.name}}</h3>
            <strong>{{food.price}}</strong>
            <div class="ele-buy">
              <ele-buy :food="food"></ele-buy>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <!-- 遮罩层 -->
    <transition name="fade">
      <div class="mask" v-show="show"></div>
    </transition>
  </div>
</template>
<script>
import Buy from '../Buy/Buy'
export default {
  data(){
    return{
      show:false,
    }
  },
  name: "cart",
  props:{
    cartGoods:{
      type:Array,
      required:true
    },
    minPrice:{
      type:Number,
      required:true
    },
    deliveryPrice:{
      type:Number,
      required:true
    },
  },
  components:{
    "ele-buy":Buy,
  },
  computed:{
    count(){//商品总数
      let cnt = 0;
      this.cartGoods.forEach(item=>{
        cnt+=item.count;
      });
      return cnt;
    },
    total(){//商品总价
      let sum = 0;
      this.cartGoods.forEach(item=>{
        sum+=item.price*item.count;
      });
      return sum;
    },
    payDesc(){//获取结算的描述信息
      if(this.count==0){
        return `¥${this.minPrice}元起送`;
      }else if(this.total <this.minPrice){
        let dif = this.minPrice - this.total;
        return `还差¥${dif}元起送`
      }else{
        return "去结算";
      }
    },
  },
  methods:{
    toggleList(){
      this.show = this.count ? !this.show : this.show;
    },
    clear(){
      this.cartGoods.forEach(item=>{
        item.count = 0;
        this.show = false;
      });
    },
  },
}
</script>
<style lang="less" scoped>
.slide-enter,.slide-leave-active{transform: translateY(100%);}
.slide-enter-active,.slide-leave-active{transition: all .5s;}
.fade-enter,.fade-leave-active{transform: translateY(100%);}
.fade-enter-active,.fade-leave-active{transition: all .5s;}
#cart{
  position: fixed;
  z-index: 100;
  left: 0;
  right: 0;
  bottom: 0;
  height:48px;
  background: #141d27;
  display: flex;
  align-items: center;
  .cart-left{
    width: 80px;
    height: 48px;
    position: relative;
    .cart-outer{
      width: 56px;
      height: 56px;
      border-radius: 50%;
      background: #141d27;
      position: absolute;
      left: 12px;
      top: -10px;
      .cart-inner{
        width: 44px;
        height: 44px;
        border-radius: 50%;
        background: rgba(255, 255, 255, .2);
        position: absolute;
        left:6px;
        top: 6px;
        text-align: center;
        line-height: 44px;
        i{
          font-size: 24px;
          color:rgba(255, 255, 255, .4);
        }
        &.active{
          background: #00a0dc;
          i{
            color: #fff;
          }
        }
      }
      .count{
        position: absolute;
        right: 0;
        top: 0;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        background:#f00;
        color: #fff;
        text-align: center;
        line-height: 20px;
        font-size: 10px;
      }
    }
  }
  .cart-right{
    width: 105px;
    height: 48px;
    line-height: 48px;
    text-align: center;
    font-size: 12px;
    font-weight: 700;
    color: rgba(255, 255, 255, .4);
    &.active{
      background: #00b43c;
      color: #fff;
    }
  }
  .cart-md{
    flex-grow: 1;
    font-size: 16px;
    color: rgba(255, 255, 255, .4);
    font-weight: normal;
    strong{
      font-weight: 700;
      border-right: 1px solid rgba(255, 255, 255, .1);
      padding-right: 12px;
      margin-right: 12px;
    }
  }
}
.cart-list{
  position: fixed;
  z-index: 90;
  left: 0;
  right: 0;
  bottom: 48px;
  background: #fff;
  .cart-list-hd{
    background: #f3f5f7;
    padding: 0 18px;
    height: 40px;
    line-height: 40px;
    border-bottom: 1px solid rgba(7,17,27,.1 );
    position: relative;
    h2{
      font-size: 14px;
      color: rgb(7, 17, 27);
    }
    span{
      position: absolute;
      right: 18px;
      top: 0;
      color: rgb(0, 160, 220);
      font-size: 12px;
    }
  }
  .cart-list-bd{
    padding: 0 18px;
    li{
      border-bottom: 1px solid rgba(7,17,27,.1);
      padding: 12px 0;
      position: relative;
      h3{
        font-size: 14px;
        color: rgb(7,17,27);
        line-height: 24px;
      }
      .ele-buy{
        position: absolute;
        right: 0;
        top: 12px;
      }
      strong{
        position: absolute;
        right: 85px;
        top: 16px;
        color: rgb(240,20,20);
        font-size: 14px;
        font-weight: 700;
      }
    }
  }
}
.mask{
  position: fixed;
  z-index: 80;
  background: rgba(7,17,27,0.6);
  left: 0;
  right: 0;
  top: 0;
  bottom: 48px;
}
</style>
