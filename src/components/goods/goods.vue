<template>
<div class=goods> 
  <div class='menu-wrapper'></div>
  <div class="foods-wrapper"></div>
</div>
</template>
<script>
import axios from 'axios'
export default {
  name:'goods',
  props:['seller'],
  data(){
    return{
      goods:[]
    }
  },
  created(){
    axios.get('http://192.168.0.174:8080/static/data.json').then(Response=>{
      this.goods=Response.data.goods
      console.dir(this.goods)
    }).catch(error=>{
      console.log(error)
    })
  }
}
</script>
<style lang="stylus" scoped>
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
  .foods-wrapper
    flex 1


</style>

