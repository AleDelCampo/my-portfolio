<script>


import AppFooter from './components/AppFooter.vue';
import AppHeader from './components/AppHeader.vue';


export default {

  data() {
    return {
      
    } 
  },
  
  components: {
    AppFooter,
    AppHeader
  },

  mounted() {

  },

  methods: {

  },
}

</script>

<template>

 <AppHeader></AppHeader>

  <div class="py-5 bg-home">

    <router-view></router-view>

  </div>

  <AppFooter></AppFooter>

</template>

<style lang="scss" scoped>
 .bg-home {
    background-color: #836fff;
  }
</style>