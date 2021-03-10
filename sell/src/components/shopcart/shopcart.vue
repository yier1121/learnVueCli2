<template>
  <div class='shopcart'>
      <div class='content'>
          <div class='content-left'>
              <div class='logo-wrapper'>
                  <div class='logo' >
                    <i class='icon-shopping_cart'></i>
                  </div>
                  <div class='num'></div>
              </div>
              <div class='price'>￥0</div>
              <div class='desc'>另需配送费0￥</div>             

          </div>
          <div class='content-right'>
              <div class='pay'>20起送</div>
          </div>
      </div>
      <div class='ball-container'>
          <div class='food-cart'>
            <div class='desc'>
                <div class='shop-cart'>购物车</div>
                <div  class='clear'>清空</div>
            </div>  
            <ul>
                <li v-for='(item,index) in foodcart' :key='index' class='food-item'>
                    <span class='item'>{{item}}</span>  
                      
                </li>
            </ul>
              

          </div>
      </div>
  </div>
</template>

<script>
export default {
    data() {
        return{
            foodcart: ['莲子核桃黑米粥','莲子核桃黑米粥','莲子核桃黑米粥']
        }
    }

}

</script>
<style lang='stylus' rel='stylesheet/stylus'>
    .shopcart 
        position: fixed 
        left: 0 
        bottom: 0
        width: 100% 
        height: 48px
        z-index: 100
        .content 
            display: flex
            background: #141d27
            color: rgba(255,255,255,.4)
            // font-size: 0
            .content-left 
                flex: 1 
                .logo-wrapper
                    display: inline-block
                    vertical-align: top
                    position: relative 
                    top: -10px
                    margin: 0 16px
                    padding: 6px 
                    width: 56px 
                    height: 56px
                    box-sizing: border-box
                    border-radius: 50%  
                    background: #141d27
                    .logo 
                        width: 100% 
                        height: 100% 
                        border-radius: 50%
                        background: #2b343c
                        text-align: center
                        line-height: 48px
                        .icon-shopping_cart
                            font-size: 24px
                
                .price 
                    display: inline-block
                    vertical-align: top
                    margin-top: 12px 
                    padding-right: 16px 
                    line-height: 24px 
                    boxing-sizing: border-box 
                    border-right: 1px solid rgba(255,255,255,0.1)
                    font-size: 16px 
                    font-weight: 700

                .desc 
                    display: inline-block
                    vertical-align: top
                    margin: 12px 0 0 12px 
                    line-height: 24px 
                    font-size: 10px

            .content-right 
                flex: 0 0 105px 
                width: 105px
                .pay 
                    height: 48px 
                    line-height: 48px 
                    text-align: center
                    font-size: 12px
                    font-weight: 700
                    background: #2b333b
        .ball-container 
            position: fixed 
            width: 100% 
            height: 100%
            top: 0 
            left 0
            z-index: 49
            background: rgba(7,17,27,0.5)
            .food-cart 
                position: absolute 
                width: 100%
                right: 0 
                bottom: 48px
                .desc 
                    width: 100% 
                    height: 40px
                    line-height: 40px
                    background: #fff 
                    font-size: 0  
                    padding: 0 12px
                    box-sizing: border-box
                    .shop-cart 
                        display: inline-block 
                        width: 50%
                        font-size: 16px 
                        text-align: left 
                        
                    .clear 
                        display: inline-block 
                        width: 50%
                        text-align: right
                        font-size: 14px
                        


                .food-item 
                    display: table
                    width: 100%
                    height: 56px
                    background: #fff
                    padding-left: 16px
                    .item 
                        display: table-cell
                        width: 100%
                        vertical-align: middle
                        border-top: 1px solid rgba(7,17,27,0.1)


                
                
                


        　

</style>