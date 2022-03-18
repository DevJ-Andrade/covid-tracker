<template>

<div class="container ">
  <Header />
  <router-view/>
</div>

</template>

<script>
import Header from '@/components/Header'

export default {
  components:{
     Header
  }
}

</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
