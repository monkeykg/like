<template>
  <div class="shopcar">
      <div class="content">
          <div class="content-left">
              <div class="logo-wrapper">
                  <div class="logo">
                      <span class="iconfont icon-gouwuche"></span>
                  </div>
              </div>
              <div class="price">￥{{totalPrice}}</div>
              <div class="desc">配送费￥{{deliveryPrice}}元</div>
          </div>
          <div class="content-right">
              <div class="pay">
                  ￥{{minPrice}}元起送
              </div>
          </div>
      </div>
  </div>
</template>
<script>
export default {
  name:'shopcar',
//  props:['deliveryPrice','minPrice','selectFoods'],
props:{
    selectFoods:{
        type:Array,
        default(){
            return [{
                price:10,
                count:1
            }];
        }
        },
    deliveryPrice:{
        default:0,
        type:Number
    },
    minPrice:{
        default:0,
        type:Number
    },
},
 computed:{
     totalPrice(){
         let total=0;
         this.selectFoods.forEach((food)=>{
             total+=food.price*food.count
         })
         return total;
     }
 }
}
</script>
<style lang="stylus">
.shopcar
    position fixed
    bottom 0
    left 0
    z-index 50
    width 100%
    height 48px
    .content
        display flex
        background #141d27
        font-size 0
        .content-left
            flex 1
            .logo-wrapper
                display inline-block
                position relative
                top:-10px
                margin 0 12px
                padding 6px
                width 56px
                height 56px
                box-sizing border-box
                vertical-align top
                border-radius 50%
                background #141d27
                .logo
                   width 100%
                   height 100%
                   border-radius 50%
                   background #2b343c
                   text-align center
                   .iconfont
                       font-size 24px
                       color #80858a
                       line-height 44px
            .price
                display inline-block
                vertical-align top
                line-height 24px
                margin-top 12px
                padding-right 12px
                border-right 1px solid rgba(255,255,255,0.1)
                font-size 16px
                font-weight 700
                color rgba(255,255,255,0.4)
            .desc    
                display inline-block  
                vertical-align top
                line-height 24px 
                margin 12px 0 0 12px
                color rgba(255,255,255,0.4)
                font-size 10px
        .content-right 
            flex 0 0 105px
            width 105px
            .pay
                font-size 12px
                height 48px
                line-height 48px
                color rgba(255,255,255,0.4)
                font-weight 700
                background #2b333b
                text-align center


</style>

