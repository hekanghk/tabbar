<template>
  <div id="App">
    <router-view></router-view>
<!--    <router-link :to="'/user/'+userId">首页</router-link>-->
    <main-tab-bar/>
  </div>
</template>

<script>
  import MainTabBar from "./components/content/MainTabBar";

  export default {
    name: 'App',
    data(){
      return {
        userId: 'hk'
      }
    },
    components: {
      MainTabBar
    }
  }
</script>

<style>
</style>
