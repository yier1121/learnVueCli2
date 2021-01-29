<template>
  <div id="app">
    <v-header :seller='seller'></v-header>
    <div class='tab '>
      <div class='tab-item'>
        <router-link to='/goods' class='rLink'>商品</router-link></div>
      <div class='tab-item'>
        <router-link to='/ratings' class='rLink'>评论</router-link></div>
      <div class='tab-item'>
        <router-link to='/seller' class='rLink'>商家</router-link>
      </div>

    </div>
    <!-- 路由匹配到的组件将渲染到这里 <router-view/>-->
  <router-view></router-view>  

  </div>
</template>

<script>
import header from './components/header/header.vue';
const ERR_OK = 0;
export default {
  name: 'App',
  data() {
    return {
      seller: {}
    };
  },
  created() {
    // this.$http.get('/api/seller').then((response) => {
    //   response = response.body;//相当于网络请求返回的json对象
    //   console.log(response);
    //   if(response.errno === ERR_OK) {
    //     this.seller = response.data;
    //     console.log(this.seller);
    //   }
    // });
    this.$http.get('/api/seller').then((response)=>{
      response=response.body;
      if(response.errno === ERR_OK) {
        this.seller = response.data;

      }
    });
  },
  components: {
    "v-header":header,
  }
}
</script>

<style lang='stylus' rel='stylesheet/stylus' >
@import './common/stylus/mixin.styl'
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex: 1
        text-align: center
        & > .rLink  
          display: block
          font-size: 14px
          color: rgb(77,85,93)        
        & > .router-link-active
          color: red

</style>
