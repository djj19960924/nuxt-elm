<template>
  <div class="home-page">
    <mt-header fixed title="静安区">
      <mt-button @click="$router.push('/search')" icon="search" slot="right"></mt-button>
    </mt-header>
    <nav class="nav-container">
      <div class="nav-item"  v-for="(item, index) in navList" :key="index">
        <img :src="item.imgUrl" alt="">
        {{item.text}}
      </div>
    </nav>
    <div class="show-list">
      <a href="https://h5.ele.me/ranking/#type=quality_meal&activity_id=1&title=%E5%93%81%E8%B4%A8%E5%A5%97%E9%A4%90&navType=0&geohash=wtw3ycy6v7pe">
        <img src="~/assets/images/show1.png" alt="">
      </a>
      <a href="https://h5.ele.me/sales/#geohash=wtw3ycy6v7pe">
        <img src="~/assets/images/show2.png" alt="">
      </a>
    </div>
    <div style="height:20px;clear:both"></div>
    <p class="shoplist-title">—— 推荐商家 ——</p>
    <ShopList />
    <Tabbar page='0' />
  </div>
</template>

<script>
  import Tabbar from '~/components/tabbar';
  import ShopList from '~/components/shopList';
  import config from '~/config';
  import { getHomeData } from '~/assets/services/common'

  export default {
    components: {
      Tabbar,
      ShopList
    },
    data () {
      return {
        data:'静安区',
        navList:[]
      }
    },
    async asyncData() {
      const res = await getHomeData();
      res.data.map((item)=>{
        item.imgUrl = config.IMG_URL+item.imgUrl;
      })
      return { navList: res.data }
    }
  }
</script>

<style lang="scss">
  @import '../assets/styles/mixin';

  .home-page {
    background-color: #fff;
    padding: px2rem(88px) 0 53px 0;
    .nav-container {
      @include fj();
      flex-wrap: wrap;
      margin-bottom: px2rem(30px);
      .nav-item {
        @include wh(20%,80px);
        text-align: center;
        color: #666;
        font-size: px2rem(24px);
        padding-top: px2rem(10px);
        img {
          display: block;
          margin: 0 auto;
          @include wh(50px, 50px);
        }
      }
    }
    .shoplist-title {
      @include fj(center);
      font-size: px2rem(30px);
      margin-bottom: px2rem(20px);
    }
    .show-list {
      padding: 0 0.4rem;
      a {
        display: inline-block;
        width: 49%;
        height: auto;
        float: left;
        &:nth-last-of-type(1) {
          float: right;
        }
      }
    }
  }
</style>

