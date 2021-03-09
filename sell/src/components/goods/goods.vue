<template>
  <div class='goods'>
    <div class='menu-wrapper' ref='menuWrapper' >
      <ul>
        <li v-for='(item,index) in goods' :key='index' class='menu-item' :class="{'current':currentIndex === index}" @click='selectMenu(index,$event)'>
          <span class='text'>
            <span class='icon' v-show='item.type>0' :class='classMap[item.type]'></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class='foods-wrapper'  ref='foodsWrapper'>
      <ul>
        <li v-for='(item,index) in goods' :key='index' class='food-list-hook'>
          <h1 class='title'>{{item.name}}</h1>
          <ul>
            <li v-for='(food,index2) in item.foods' class='item-food' :key='index2'>
              <div class='icon'>
                <img width:="57" height="57" :src='food.icon'>
              </div>
              <div class='content'>
                <h2 class='name'>{{food.name}}</h2>
                <p class='desc'>{{food.description}}</p>
                <div class='extra'>
                  <span class='count'>月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class='price'>
                  <span class='now'>${{food.price}}</span>
                  <span class='old' v-show='food.oldPrice'>{{food.oldPrice}}</span>
                </div>
                <div class='addfoods'>
                  <i class='icon-remove_circle_outline' v-show='count > 0'  @click='()=>{count--}'></i>
                  <span class='count'>{{count}}</span>
                  <i class='icon-add_circle' @click ='()=>{count++}'></i>

                  <span></span>
                </div>
                </div>

            </li>
          </ul>
        </li>
      </ul>
    </div>
    <div class='shopchart'>
      <div class='cart'><span class='icon-shopping_cart'></span></div>
      <div class='totalprice'>$20</div>
      <div class='peisong'>另需配送费2$</div>
      <div class='qisong'>$20起送</div>
      
    </div>

  </div>
</template>

<script>
import BScroll from 'better-scroll'
const ERR_OK = 0;

export default {
    // name: 'goods'
    props: {
      seller:{

      }
    },
    data() {
      return{
        goods: [],
        listHeight: [],
        scrollY: 0,
        count: 0
        
      }
    },
    computed:{
      currentIndex() {
        for(let i=0;i<this.listHeight.length;i++) {
          let height1=this.listHeight[i]
          let height2=this.listHeight[i+1]
          if(!height2 || (this.scrollY >= height1 && this.scrollY <=height2)) {
            // alert(i)
            return i 

          }
          
        }
        return 0

      }
    },
    created() {
      this.classMap=['decrease','discount','special','invoice','guarantee'];
      this.$http.get('/api/goods').then((response)=>{
      response=response.body;
      if(response.errno === ERR_OK) {
        this.goods = response.data;
        this.$nextTick(()=>{
          this._initScroll()
          this._calculateHeight()
        })
        
       

      }
    });
    },
    methods: {
      selectMenu(index,event) {
        if(!event._constructed) {
          return;
        }
        let foodslist = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook')
        let el = foodslist[index]
        this.foodsScroll.scrollToElement(el,0.3*1000)
  },
      _initScroll() {
        this.menuScroll = new BScroll(this.$refs.menuWrapper,{
          click: true
        })
        this.foodsScroll = new BScroll(this.$refs.foodsWrapper,{
          click: true,
          probeType: 3
        })
        this.foodsScroll.on('scroll',(pos)=>{
          this.scrollY = Math.abs(Math.round(pos.y))
        })
        
      },
      _calculateHeight() {
        let foodlist = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook')
        let height = 0
        this.listHeight.push(height)
        for(let i=0;i<foodlist.length;i++) {
          let item = foodlist[i]
          height +=item.clientHeight 
          this.listHeight.push(height)
        }
         


      }

    }

}

</script>
<style lang='stylus' rel='stylesheet/stylus'>
  @import '../../common/stylus/mixin.styl'
  .goods 
    position: absolute 
    top: 174px 
    bottom: 48px 
    display: flex 
    overflow: hidden
    .menu-wrapper 
      flex: 0 0 80px 
      width: 80px 
      background: #f3f5f7
      .menu-item 
        display: table 
        height: 54px 
        width: 56px 
        line-height: 14px 
        padding: 0 12px
        &.current 
          position: relative 
          margin-top: -1px 
          z-index: 10 
          font-weight: 700 
          background: #fff
          .text
            border-none()
        .icon 
          display: inline-block
          vertical-align: top
          width: 12px
          height: 12px
          margin-right: 2px
          background-size: 12px 12px
          background-repeat: no-repeat
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.guarantee
            bg-image('guarantee_3')
          &.invoice
            bg-image('invoice_3')
          &.special
            bg-image('special_3')
        .text 
          display: table-cell 
          width: 56px 
          vertical-align: middle 
          border-1px(rgba(7,17,27,0.1))
          font-size: 12px 

    .foods-wrapper
      flex: 1 
      .title 
        padding-left: 14px 
        border-left: 2px solid #d9dde1
        height: 26px 
        line-height: 26px
        font-size: 12px
        color: rgb(147, 153, 159)
        background-color: #f3f5f7
      .item-food
        display: flex 
        margin: 18px 
        padding-bottom: 18px 
        border-1px(rgba(7,17,27,0.1))
        &: last-child 
          margin-bottom: 0 
          border-none()
        .icon 
          flex: 0 0 57px 
          // width: 57px 
          margin-right: 10px 
        .content 
          flex: 1
          position: relative
          .name 
            margin: 2px 0 8px 0
            height: 14px 
            line-height: 14px 
            font-size: 14px
            color: rgb(7,17,27)
          .desc, .extra
            line-height: 10px 
            font-size: 10px 
            color: rgb(147,153,159)
          .desc 
            margin-bottom: 8px 
            line-height: 12px 
          .extra 
            .count 
              margin-right: 12px             
          .price 
            font-weight: 700 
            line-height: 24px
          .addfoods 
            position: absolute
            right: 2px
            bottom: 2px

            .now 
              margin-right: 8px 
              font-size: 14px 
              color: rgb(240,20,20)
            .old 
              text-decoration: line-through 
              font-size: 10px 
              color: rgb(147,153,159)
  .shopchart
    display: flex
    position: fixed 
    height: 48px
    line-height: 48px
    text-align: center
    width: 100%
    bottom: 0
    right: 0
    background: rgba(7,17,27,0.5)    
    .cart
      flex: 0 0 12.5%
    .totalprice
      flex: 0 0 12.5%
    .peisong 
      flex: 0 0 50%
    .qisong 
      border-left: 1px solid #fff
      flex: 0 0 25%      

            




          




        
</style>