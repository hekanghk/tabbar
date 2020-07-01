<template>
  <div id="home">
    <NavBar><div slot="center">购物街</div></NavBar>
    <scroll class="content" ref="scroll">
      <home-swiper :banners="banners"/>
      <tab-control :titles="['流行','新款','精选']"></tab-control>
      <goods-list :goods="goods['pop'].list"></goods-list>
    </scroll>
    <back-top @click.native="backClick"></back-top>
  </div>
</template>

<script>
  import NavBar from "../../components/common/navbar/NavBar";
  import GoodsList from "../../components/content/goods/GoodsList";
  import TabControl from "../../components/content/tabControl/TabControl";
  import Scroll from "../../components/common/scroll/Scroll";
  import BackTop from "../../components/content/backTop/BackTop";

  import {getHomeGoods, getHomeMultidata} from "../../network/home";

  import HomeSwiper from "./childComps/HomeSwiper";

  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwiper,
      GoodsList,
      TabControl,
      Scroll,
      BackTop
    },
    data() {
      return {
        banners: [],
        recommends: [],
        goods: {
          'pop': {page: 0, list: []},
          'new': {page: 0, list: []},
          'sell': {page: 0, list: []},
        }
      }
    },
    created() {
      this.getHomeMultidata()

      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    methods: {
      backClick(){     //分别是   组件  属性  属性的方法
        this.$refs.scroll.scroll.scrollTo(0, 0, 1000)
      },
      getHomeMultidata()
      {
        getHomeMultidata().then(res => {
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type)
      {
        const page = this.goods[type].page + 1
        getHomeGoods(type, page).then(res => {
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1
        })
      },
    }
  }
</script>

<style scoped>
  .content{
    height: 100px;
  }
</style>