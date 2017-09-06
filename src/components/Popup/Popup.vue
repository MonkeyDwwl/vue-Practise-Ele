<template>
  <div id="popup">
    <h1>{{seller.name}}</h1>
    <div class="xing">

    </div>
    <div class="discount">
      <h2><i></i><strong>优惠信息</strong><i></i></h2>
      <ul>
        <li v-for="(item,index) in seller.supports" :key="index"><em></em>{{item.description}}</li>
      </ul>
    </div>
    <div class="bulletin">
      <h2><i></i><strong>商家公告</strong><i></i></h2>
      <p>{{seller.bulletin}}</p>
    </div>
    <!-- 关闭按钮 -->
    <div class="close" @click="close">
      x
    </div>
  </div>
</template>
<script>
export default {
  name: "popup",
  methods: {
    close() {
      this.$emit('close');
    },
  },
  props: {
    seller : {
      type : Object,
      required : true
    }
  },
}
</script>
<style lang="less" scoped>
#popup{
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  background: rgba(7,17,27,.8);
  color:#fff;
  z-index: 10;
  h1{
    margin-top: 64px;
    text-align: center;
    font-size: 16px;
    font-weight: 700;
  }
  .discount,.bulletin{
    margin:28px 36px;
    font-size: 12px;
    font-weight: 200;
    h2{
      text-align: center;
      line-height: 50px;
      font-size: 14px;
      font-weight: 700;
    }
  }
  .discount{
    h2{
      display: flex;
      align-items: center;
      i{
        width: 110px;
        height: 2px;
        background-color: rgba(255,255,255,.2);
        display: inline-block;
        vertical-align: top;
      }
      strong{
        padding: 0 12px;
      }
    }
    li{
      padding: 6px 0;
      em{
        background: url('./special_1@2x.png') no-repeat;
        background-size: contain;
        display: inline-block;
        width: 16px;
        height: 16px;
        vertical-align: top;
        margin-right: 6px;
      }
    }
  }
  .bulletin{
    p{
      line-height: 24px;
    }
    h2{
      display: flex;
      align-items: center;
      i{
        width: 110px;
        height: 2px;
        background-color: rgba(255,255,255,.2);
        display: inline-block;
        vertical-align: top;
      }
      strong{
        padding: 0 12px;
      }
    }
  }
  .close{
    font-size: 32px;
    color: rgba(255, 255, 255, .5);
    position: absolute;
    bottom: 32px;
    left: 50%;
    transform: translateX(-50%);
  }
}
</style>
