<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if='!isActive'><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :class="{active: isActive}"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
  export default {
    name: "TabBarItem.vue",
    props:{
      link: String
    },
    // data(){
    //   return{
    //     isActive: false
    //   }
    // },
    methods:{
      itemClick(){
        this.$router.replace(this.link)
      }
    },
    computed:{
      isActive(){
        return this.$route.path.includes(this.link)
      }
    }
  }
</script>

<style scoped>
  .tab-bar-item{
    flex: 1;
    text-align: center;
    height: 49px;
  }

  .tab-bar-item img{
    width: 24px;
    height: 24px
  }

  .active{
    color:red
  }
</style>