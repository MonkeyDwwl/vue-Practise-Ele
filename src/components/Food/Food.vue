<template>
  <div id="food">
    <div id="foodinfo">
      <ul>
        <li class="back" @click="close">
          &lt;
        </li>
        <li class="pic">
          <img :src="food.image" alt="">
        </li>
        <li class="info">
          <h1>{{food.name}}</h1>
          <p class="sale">月售{{food.sellCount}}份 好评率{{food.rating}}</p>
          <p class="price">
            <strong><span>¥</span>{{food.price}}</strong>
            <del v-if="food.oldPrice">{{food.oldPrice}}</del>
          </p>
        </li>
        <li class="line"></li>
        <li class="intro">
          <h2>商品介绍</h2>
          <p>{{food.info}}</p>
        </li>
        <li class="line"></li>
        <li class="ratings">
          <h2>商品评价</h2>
          <ul>
            <li v-for="(item,index) in food.ratings">{{item.text}}</li>
          </ul>
        </li>
        <li class="line"></li>
        <li class="ratings">
          <h2>商品评价</h2>
          <ul>
            <li v-for="(item,index) in food.ratings">{{item.text}}</li>
          </ul>
        </li>
        <li class="line"></li>
        <li class="ratings">
          <h2>商品评价</h2>
          <ul>
            <li v-for="(item,index) in food.ratings">{{item.text}}</li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import IScroll from '../../../static/js/iscroll-probe.js'

export default {
  name: "food",
  props:{
    food : {
      type :Object,
      required : true,
    }
  },
  methods:{
    close(){
      this.$emit('close');
    },
  },
  mounted() {
    //do something after mounting vue instance
    var myscroll = new IScroll("#foodinfo",{click:true,probeType:2});
    setTimeout(function(){
        myscroll.refresh();
    },0);

  },
}
</script>
<style lang="less" scoped>
#food{
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #fff;
  #foodinfo{
    width: 100%;
    height: 100%;
    .back{
      position: absolute;
      left: 20px;
      top: 15px;
      font-size: 32px;
      color: #f00;
    }
    .pic{
      height: 375px;
      img{
        width: 100%;
        height: 375px;
      }
    }
    .info,.intro,.ratings{
      margin:18px;
    }
    .info{
      h1{
        font-size: 16px;
        font-weight: bold;
        color: rgb(7, 17, 27);
      }
      .sale{
        font-size: 10px;
        color: rgb(147, 153, 159);
        magrgin:8px 0;
      }
      .price{
        strong{
          color: rgb(240, 20, 20);
          font-size: 14px;
          font-weight: 700;
          span{
            font-size: 10px;
            font-weight: normal;
          }
        }
        del{
          font-size: 10px;
          color: rgb(147,153, 159);
        }
      }
    }
    .line{
      height: 16px;
      background: #f3f5f7;
      border: 1px solid rgba(7, 17, 27, .1);
      border-left: none;
      border-right: none;
    }
    .intro,.ratings {
        h2 {
            color: rgb(7,17,27);
            font-weight: 700;
            font-size: 12px;
            margin-bottom: 10px;
        }
    }
    .intro {
        p {
            font-size: 12px;
            line-height: 24px;
            color: rgb(77,85,93);
        }
    }
  }

}
</style>
