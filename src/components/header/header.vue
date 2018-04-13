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
            <div class='support-count' v-if="seller.supports" @click="showDetail">
                <span class="count">{{seller.supports.length}}个</span>
                <i class="icon-gengduo iconfont"></i>
            </div>
         </div> 
      </div>
      <div class='bulletin-wrapper'  @click="showDetail">
        <span class="bulletin-title"></span>
        <span class="bulletin-text">{{seller.bulletin}}</span>
        <i class="icon-gengduo iconfont"></i>
      </div>
      <div class="background">
          <img :src="seller.avatar" alt="" width='100%' height='100%'>
      </div>
      <div class="detail" v-show="detailShow">
          <div class="detail-wrapper clearfix"> 
              <div class='detail-main'> 
                  <h1 class="name">{{seller.name}}</h1>
              </div>
          </div>
          <div class='detail-close' @click="closeDetail"> 
              <i class='icon-guanbi iconfont'></i>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name:'Header',
  props:['seller'],
  data(){
      return{
          classMap:['decrease','discount','special','invoice','guarantee'],
            detailShow:false
      }
  },
methods:{
showDetail:function(){
    this.detailShow=true
},
closeDetail(){
    this.detailShow=false
}
}
}
</script>
<style lang="stylus" scoped>
@import "../../common/stylus/mixin"

.header
    color:#fff
    background rgba(7,17,27,0.5)
    position relative
    .content-wrapper
        padding 24px 12px 18px 24px
        font-size 0
        position  relative
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
            .support-count
                position absolute 
                right 12px
                bottom 18px
                padding 0 8px
                height 24px
                line-height 24px 
                border-radius 14px 
                background rgba(0,0,0,0.2)
                text-align center
                .count
                    font-size 10px
                .iconfont
                    font-size 10px    
    .bulletin-wrapper
        height 28px
        line-height 28px
        padding 0 22px 0 12px
        position relative
        white-space nowrap
        overflow hidden
        text-overflow ellipsis
        background rgba(7,17,27,0.2)
        .bulletin-title
            display inline-block
            width 22px
            height 12px
            bg-img('bulletin')
            background-repeat no-repeat
            background-size 22px 12px
        .bulletin-text
            font-size 10px  
            margin 0 4px
        .iconfont
            position absolute 
            font-size 10px  
            right 12px
            top 4px
    .background
        position absolute  
        top 0
        left 0
        width 100%
        height 100%
        z-index -1
        filter blur(10px)
    .detail
        position fixed
        top 0
        left 0
        z-index 100
        height 100%
        width 100%
        overflow-y  auto 
        background rgba(7,17,27,0.8)
        // filter blur(10px)
        .detail-wrapper
            min-height 100%
            width 100%
            .detail-main
                margin-top 64px
                padding-bottom 64px
                .name
                    font-weight 700
                    font-size 16px
                    line-height 16px
                    color rgb(255,255,255)
                    text-align center

        .detail-close
            position relative
            width 32px
            height 32px
            margin -64px auto 0 auto
            clear both
            font-size 32px
            .icon-guanbi
                color rgb(225,225,225,0.5)






                    
                    




</style>



