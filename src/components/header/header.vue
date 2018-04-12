<template>
  <div class='header'>
      <div class='content-wrapper'>
         <div class='avater'>
            <img :src="seller.avatar" alt="" width="64" height="64"> 
         </div>
         <div class="content">
            <div class="title">
                <span class='brand'></span>    
                <span class='name'>{{seller.name}}</span>    
            </div> 
            <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>  
            <div v-if="seller.supports" class='supports'>
                <span class="icon"></span>
                <span class='text'>{{seller.supports[0].description}}</span>
            </div>
         </div> 
      </div>
      <div class='bulletin-wrapper'></div>
  </div>
</template>

<script>
export default {
  name:'Header',
  props:['seller']
}
</script>
<style lang="stylus">

</style>


