<template>
  <div id="home">
    <nav-bar class="nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <swiper>
      <swiper-item v-for="item in banners" :key="item.link">
        <a v-bind:href="item.link">
          <img v-bind:src="item.image" alt="">
        </a>
      </swiper-item>
    </swiper>
    <recommend :recommends="recommends"></recommend>
  </div>

</template>

<script>
  import navBar from '../../components/navbar/NavBar'
  import {getHomeMultidata} from '@/network/home'
  import {Swiper, SwiperItem} from '../../components/swiper/index'
  import Recommend from "@/views/home/homeChild/Recommend";
  export default {
    name: "Home",
    components:{
      Recommend,
      navBar,
      Swiper,
      SwiperItem,
    },
    data(){
      return{
        banners:[],
        recommends:[]

      }
    },
    created() {
      getHomeMultidata().then(res=>{
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      }).catch(err=>{
        console.log(err)
      })

    }
  }
</script>

<style scoped>
.nav{
  background-color: var(--color-tint);
  color: #f6f6f6;
}
</style>
