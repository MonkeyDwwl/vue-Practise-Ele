<template lang="html">
  <div class="goods">
    <!-- 左边的分类 -->
    <div class="goods-menu" id="goods-menu">
      <ul>
        <li v-for="(item,index) in goods" :key="index" :class="{active:index===current}"
         @click="selectCategory(index)">
          <p>{{item.name}}</p>
        </li>
      </ul>
    </div>
    <!-- 右边商品列表 -->
    <div class="goods-list" id="goods-list">
      <div ref="list">
        <dl v-for="(item,index) in goods" :key="index">
          <dt>{{item.name}}</dt>
          <dd v-for="(food,idx) in item.foods" :key="idx" @click="selectFood(food)">
            <img :src="food.icon" alt="">
            <div class="food">
              <h2>{{food.name}}</h2>
              <p class="desc" v-if="food.description">{{food.description}}</p>
              <p class="sale">月售{{food.sellCount}}份 好评率{{food.rating}}</p>
              <p class="price">
                <strong><span>¥</span>{{food.price}}</strong>
                <del v-if="food.oldPrice">¥{{food.oldPrice}}</del>
              </p>
              <!-- 添加购物车组件 -->
              <div class="ele-buy">
                <ele-buy :food="food"></ele-buy>
              </div>
            </div>
          </dd>
        </dl>
      </div>
    </div>
    <!-- 商品详情页 -->
    <transition name="slide">
        <ele-food v-if="show" @close="show=false" :food="currentFood"></ele-food>
    </transition>

    <!-- 购物车组件 -->
    <ele-cart :cartGoods = "cartGoods"
      :minPrice = "seller.minPrice"
        :deliveryPrice = "seller.deliveryPrice"

    ></ele-cart>
  </div>
</template>

<script>
import IScroll from '../../../static/js/iscroll-probe'
import Food from '../Food/Food'
import Buy from '../Buy/Buy'
import Cart from '../Cart/Cart'
const shop = require('../../api/data.json')

export default {
  data(){
    return{
      goods:[],//该商家所有的外卖商品
      current:0,//定义当前所在的分类,默认为0,表示第一个分类
      listHeight:[],//表示右侧商品分类容器的高度
      show:false,
      currentFood:{},//获取当前选中的商品
    }
  },
  components:{
    'ele-food' : Food ,
    'ele-buy' : Buy,
    'ele-cart' : Cart,
  },
  methods:{
    selectCategory(index){
      this.current = index;//修改curren的值
      let dls = this.$refs.list.getElementsByTagName('dl');
      this.listScroll.scrollToElement(dls[this.current]);
    },
    //定义一个方法,计算每个商品分类的高度
    _getListHeight(){
      let arr=[0];
      //获取所有的dl
      let dls = this.$refs.list.getElementsByTagName('dl');
      for(let i=0; i<dls.length;i++){
        arr.push(dls[i].clientHeight + arr[i]);
      };
      return arr;
    },
    //点击food 进入详情页
    selectFood(food){
      this.show = true;
      this.currentFood = food;
    }
  },
  computed:{
    //获取添加到购物车中的商品
    cartGoods(){
      let cart = [];
      this.goods.forEach(item=>{
        item.foods.forEach(food=>{
          if(food.count){
            cart.push(food);
          }
        });
      });
      return cart;
    }
  },
  created() {
    //do something after creating vue instance
    this.goods = shop.goods;
    this.seller = shop.seller;
  },
  mounted() {
    //do something after mounting vue instance
    this.menuScroll = new IScroll("#goods-menu",{click:true});
    this.listScroll = new IScroll("#goods-list",{click:true,probeType:2});

    //调用_getListHeight获取商品列表容器的高度
    this.listHeight = this._getListHeight();
    //注册scroll事件
    //缓存this
    let _this = this;
    this.listScroll.on('scroll',function(){
      let dis = Math.abs(this.y);
      for(let i=0;i<_this.listHeight.length;i++){
        let start = _this.listHeight[i];
        let end = _this.listHeight[i+1];
        if(!end || (dis>=start&&dis<end)){
          _this.current = i;
          break;
        }
      }
    });
  },
}
</script>

<style lang="less" >
  .slide-enter,.slide-leave-active{transform: translateX(100%);}
  .slide-enter-active,.slide-leave-active{transition: all .3s;}
  .goods{
    position: fixed;
    left: 0;
    right: 0;
    top: 175px;
    bottom: 48px;
    overflow: hidden;
    display: flex;
    .goods-menu{
      background: #f3f5f7;
      min-width: 80px;
      width: 80px;
      li{
        height: 54px;
        padding: 0 12px;
        p{
          height: 54px;
          border-bottom: 1px solid rgba(7,17,27,.1);
          font-size: 12px;
          font-weight: 200;
          color: rgb(77, 85, 93);
          display: flex;
          align-items: center;
        }
        &.active{
          background: #fff;
          p{
            border-bottom: none;
          }
        }
      }
    }
    .goods-list{
      flex-grow: 1;
      dt{
        background-color: #f3f5f7;
        border-left: 3px solid #d9dde1;
        height: 26px;
        line-height: 26px;
        font-size: 12px;
        color:rgb(147, 153, 159);
        padding-left:14px;
      }
      dd{
        margin:18px;
        display: flex;
        img{
          width: 57px;
          height: 57px;
          margin-right: 10px;
        }
        .food{
          position: relative;
          flex-grow: 1;
          h2{
            font-size: 14px;
            color: rgb(7,17,27);
          }
          .desc,.sale{
            font-size: 10px;
            color: rgb(147,153,159);
            margin:8px 0;
          }
          .price{
            strong{
              color: rgb(240,20,20);
              font-weight: 700;
              font-size: 14px;
              span{
                font-size: 10px;
              }
            }
            del{
              color: rgb(147,153,159);
              font-weight: 700;
              font-size: 10px;
            }
          }
          .ele-buy{
            position: absolute;
            right: 0;
            bottom: 0;
          }
        }
      }
    }
  }
</style>
