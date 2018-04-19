<template>
  <div class="cartcontrol">
      <div class="cart-decrease " v-show="food.count>0" @click="decreaseCart" transition='move'>
          <span class="inner icon-53 iconfont"></span>
      </div>
      <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
      <div class="cart-add icon-jia1 iconfont" @click="addCart"></div>
  </div>
</template>
<script>
import Vue from 'vue'
export default {
  name:'cartcontrol',
props:{
    food:{
        type:Object
    }
},
created(){
    // console.log(this.food)
},
methods:{
    addCart(){
        console.log('click')
        if(!this.food.count){
            // this.food.count=1
            Vue.set(this.food,'count',1)
        }else{
           this.food.count++ ;
        }
    },
    decreaseCart(){
        this.food.count-- ;
    }
}
}
</script>
<style lang="stylus">
.cartcontrol
    font-size 0
    .cart-decrease
        display inline-block
        padding 6px
        transition  all 0.4s linear
        &.move-transition
            opacity 1
            transform translate3D(0,0,0) 
            .inner
                display inline-block
                font-size 24px
                line-height 24px 
                color rgb(0,160,220)
                transition  all 0.4s linear
                transform rotate(0)
        &.move-enter, &.move-leave
            opacity 0
            transform translate3D(24px,0,0 )  
            .inner
                transform rotate(180deg)  
    .cart-count
        display inline-block
        font-size 10px
        vertical-align top
        width 12px
        padding-top 6px
        line-height 24px
        text-align center
        color rgb(147,153,159)  
    .cart-add 
        display inline-block 
        font-size 24px
        line-height 24px 
        color rgb(0,160,220)    
</style>


