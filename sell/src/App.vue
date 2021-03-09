<template>
  <div id="app">
    <v-header :seller='seller'></v-header>
    <div class='tab'>
      <div class='tab-item'>
        <router-link to='/goods' class='rlink'>商品</router-link>
      </div>
      <div class='tab-item'>
        <router-link to='/ratings' class='rlink'>评论</router-link>
      </div>      
      <div class='tab-item'>
        <router-link to='/seller' class='rlink'>商家</router-link>
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
      .tab-item
        flex: 1
        text-align: center
        & > .rlink
          font-size: 14px
          color: #D0D0D0
        & > .router-link-active
          color: #FF0000   
        
    

</style>
