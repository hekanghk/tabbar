<template>
  <div id="tab-bar">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: "TabBar.vue"
  }
</script>

<style scoped>
  @import "../../assets/css/base.css";

  #tab-bar{
    display: flex;
    background-color: #f6f6f6;    /*添加背景灰*/

    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;     /*这四行让tabbar到页面底部*/
  }

</style>