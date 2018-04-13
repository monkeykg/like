<template>
  <div class='header'>
      <div class='content-wrapper'>
         <div class='avatar'>
            <img :src="seller.avatar" alt="" width="64" height="64"> 
         </div>
         <div class="content">
            <div class="title">
                <span class='brand'></span>    
                <span class='name'>{{seller.name}}</span>    
            </div> 
            <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>  
            <div v-if="seller.supports" class='supports'>
                <span class="icon" :class='classMap[seller.supports[0].type]'></span>
                <span class='text'>{{seller.supports[0].description}}</span>
            </div>
            <div class='support-count' v-if="seller.supports">
                <span class="count">{{seller.supports.length}}</span>
                <i></i>
            </div>
         </div> 
      </div>
      <div class='bulletin-wrapper'></div>
  </div>
</template>

<script>
export default {
  name:'Header',
  props:['seller'],
  data(){
      return{
          classMap:['decrease','discount','special','invoice','guarantee']
      }
  },

}
</script>
<style lang="stylus" scoped>
@import "../../common/stylus/mixin"

.header
    color:#fff
    background-color #000000
    .content-wrapper
        padding 24px 12px 18px 24px
        font-size 0
        .avatar
            display inline-block
            vertical-align top
            &>img 
             border-radius 2px
        .content
            display inline-block
            font-size 14px
            margin-left:16px
            .title
                margin:2px 0 8px 0  
                .brand
                    width 30px
                    height 18px  
                    display inline-block
                    vertical-align top
                    // background 
                    bg-img('brand')
                    background-size 30px 18px 
                    background-repeat no-repeat
                .name
                    font-size 16px 
                    color rgb(255,255,255)
                    font-weight bold
                    margin-left 6px
                    line-height 18px
            .description
                font-size 12px
                font-weight 200
                margin-bottom 10px   
            .supports  
                .icon
                    display inline-block
                    vertical-align top
                    width 12px
                    height 12px
                    margin-right 4px 
                    background-size 12px 12px
                    background-repeat no-repeat  
                    &.decrease
                        bg-img('decrease_1') 
                    &.discount
                        bg-img('discount_1')
                    &.guarantee
                        bg-img('guarantee_1') 
                    &.invoice
                        bg-img('invoice_1') 
                    &.special
                        bg-img('special_1')
                .text
                    font-size 12px
                    line-height 10px
                    font-weight 200





</style>



