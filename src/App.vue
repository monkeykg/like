<template>
  <div id="app">
    <v-header :seller='seller'></v-header> 
    <div class="tab">
      <div class='tab-item'>
        <router-link to="/goods">商品</router-link>
      </div>
      <div class='tab-item'>
        <router-link to="/ratings">評價</router-link>
      </div>
      <div class='tab-item'>
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller='seller'></router-view>
  </div>
</template>

<script>
import Header from "@/components/header/header.vue";
import axios from 'axios'
export default {
  name: "App",
  components: {
    'v-header':Header
  },
  data(){
    return{
      seller:{}
    }
  },
  created(){
    axios.get('http://localhost:8080/static/data.json').then(Response=>{
      this.seller=Response.data.seller;
      console.dir(this.seller)
    }).catch(error=>{
      console.log(error)
    })
  }
};
</script>
<style lang="stylus">
@import 'common/stylus/base'


#app
  .tab
    display flex
    width 100%
    height 40px
    line-height 40px
    border-bottom 1px solid rgba(7,17,27,0.1)
    .tab-item
      flex 1
      text-align center
      &>a
        display block 
        font-size 14px
        color:rgb(77,85,85)
      &>a.router-link-active
        color:rgb(240,20,20)
</style>

