<template>
<div class=goods> 
  <div class='menu-wrapper' ref='menuwrapper'>
    <ul>
      <li v-for="(val,index) in goods" class="menu-item" :class="{'current':currentIndex==index}" @click="selectMenu(index,$event)">
        <span class='text'><span v-show="val.type>0" class="icon" :class="classMap[val.type]"></span>{{val.name}}</span>
      </li>
    </ul>
  </div>
  <div class="foods-wrapper" ref='foodswrapper'>
    <ul>
      <li v-for="item in goods" class='food-list food-list-hook'>
        <h1 class="title">{{item.name}}</h1>
        <ul>
          <li class='food-item' v-for="food in item.foods">
            <div class='icon'>
              <img :src="food.icon" alt="" width='57' height='57'>
            </div>
            <div class="content">
              <h2 class="name">{{food.name}}</h2>
              <p class="desc" v-show="food.description">{{food.description}}</p>
              <div class="extra">
                <span class="count">月售{{food.sellCount}}份</span>
                <span>好评率{{food.rating}}%</span>
              </div>
              <div class='price'>
                <span class="now">￥{{food.price}}</span>
                <span class='old' v-show='food.oldPrice'>￥{{food.oldPrice}}</span>
              </div>
            </div>
          </li>
        </ul>
      </li>
    </ul>
  </div>
  <shopcar :delivery-price='seller.deliveryPrice' :min-price='seller.minPrice'></shopcar>
</div>
</template>
<script>
import axios from 'axios'
import BScroll from 'better-scroll'
import shopcar from '@/components/shopcar/shopcar.vue'
export default {
  name:'goods',
  props:['seller'],
  components:{
    shopcar
  },
  data(){
    return{
      goods:[],
      listHeight:[],
      scrollY:0,
       classMap:['decrease','discount','special','invoice','guarantee']
    }
  },
  computed:{
    currentIndex(){
      for(let i=0;i<this.listHeight.lenght;i++){
        let height1=this.listHeight[i]
        let height2=this.listHeight[i+1]
        if(!height2 ||(this.scrollY>=height1 && this.scrollY<height2)){
          return i;
        }
      }
      return 0;
    }
  },
  created(){
    axios.get('http://192.168.0.174:8080/static/data.json').then(Response=>{
      this.goods=Response.data.goods
      this.$nextTick(()=>{
         this. _initScroll();
         this._calculateHeight();
      })
     
      console.dir(this.goods)
    }).catch(error=>{
      console.log(error)
    })
  },
  methods:{
    _initScroll(){
      this.menuScroll=new BScroll(this.$refs.menuwrapper,{
        click: true
      })
      this.foodScroll=new BScroll(this.$refs.foodswrapper,{
      click: true,
       probeType: 3
      })
      this.foodScroll.on('scroll',(pos)=>{
        this.scrollY=Math.abs(Math.round(pos.y))
      })
    },
    _calculateHeight(){
      let foodList=this.$refs.foodswrapper.getElementsByClassName('food-list-hook')
      let height=0
      this.listHeight.push(height)
      for(let i=0;i< foodList.length;i++){
        let item=foodList[i]
        height+=item.clientHeight
        this.listHeight.push(height)
      }
      },
      selectMenu(index,event){
        // console.log(index)
        let foodList=this.$refs.foodswrapper.getElementsByClassName('food-list-hook');
         let el=foodList[index];
         this.foodScroll.scrollToElement(el,300)
      }
  }
}
</script>
<style lang="stylus" scoped>
@import "../../common/stylus/mixin"
.goods
  position absolute
  top 174px
  bottom 46px
  width 100%
  display flex
  overflow hidden
  .menu-wrapper
    flex 0 0 80px
    width 80px
    background #f3f5f7
    .menu-item
      display table
      height 54px
      width 56px
      line-height 14px
      padding 0 12px
      &.current
        position relative
        z-index 10
        margin-top -1px
        background #ffffff
        font-weight 700
        .text
          border none
      .icon
        display inline-block
        vertical-align top
        width 12px
        height 12px
        margin-right 2px 
        background-size 12px 12px
        background-repeat no-repeat  
        &.decrease
          bg-img('decrease_3') 
        &.discount
          bg-img('discount_3')
        &.guarantee
          bg-img('guarantee_3') 
        &.invoice
          bg-img('invoice_3') 
        &.special
          bg-img('special_3')
      .text
        font-size 12px
        display table-cell  
        width 56px
        vertical-align middle  
        border-bottom 1px solid rgba(7,17,27,0.1)
  .foods-wrapper
    flex 1
    .title
      padding-left 14px
      height 26px
      line-height 26px
      border-left 2px solid #d9dde1
      font-size 12px
      color rgb(147,153,159)
      background #f3f5f7
    .food-item
      display flex 
      margin 18px
      padding-bottom 18px
      border-bottom 1px solid rgba(7,17,27,0.1)
      &:last-child
        border 0
        margin-bottom 0
      .icon
        flex 0 0 57px
        margin-right 10px
      .content
        flex 1
        .name
          margin 2px 0 8px 0
          height 14px
          line-height 14px
          font-size 14px
          color rgb(7,17,27)
        .desc
          margin-bottom 8px
          line-height 12px
          font-size 10px
          color rgb(147,153,159)
        .extra
          height 10px
          line-height 10px
          font-size 10px
          color rgb(147,153,159)
          margin-bottom 8px
          .count
            margin-right 12px
        .price
          font-weight 700
          line-height 24px
          .now
            margin-right 18px
            font-size 14px
            color rgb(240,20,20)
          .old
            text-decoration line-through
            fone-size 10px
            color rgb(147,153,159)






</style>

