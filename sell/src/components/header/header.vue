<template>
  <div class='header'>
    <div class='content-wrapper'>
      <div class='avatar'>
        <img height='64' width='64' :src='seller.avatar'>
      </div>
      <div class='content'>
        <div class='title'>
          <span class='brand'></span>
          <span class='name'>{{seller.name}}</span>
        </div>
        <div class='description'>
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if='seller.supports' class='support'>
          <span class='icon' :class='classMap[seller.supports[0].type]'></span>
          <span class='text'>{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if='seller.supports' class='support-count'  @click='showDetail'>
        <span class='count'>{{seller.supports.length}}个</span>
        <i class='icon-keyboard_arrow_right'></i>
      </div>
    </div>
    <div class='bulletin-wrapper' @click='showDetail'>
      <span class='bulletin-title'></span><span class='bulletin-text'>{{seller.bulletin}}</span>
      <i class='icon-keyboard_arrow_right'></i>
    </div>
    <div v-show='detailShow' class='detail' clearfix transition='fade'>
      <div class='detail-wrapper'>
        <div class='detail-main'>
          <div class='name'>{{seller.name}}</div>
          <div class='star-wrapper'>
            <star :size='48' :score='seller.score' ></star>
          </div>
          <div class='title'>
            <div class='line'></div>
            <div class='text'>优惠信息</div>
            <div class='line'></div>
          </div>
          <ul v-if='seller.supports' class='supports'>
            <li  v-for='(item,index) in seller.supports' class='support-item'  :key='index'>
              <span class='icon' :class='classMap[item.type]' ></span>
              <span class='text'> {{item.description}}</span>
            </li>
          </ul>
          <div class='title'>
            <div class='line'></div>
            <div class='text'>商家公告</div>
            <div class='line'></div>
          </div>
          <div class='bulletin'>
            <p class='content'>{{seller.bulletin}}</p>
          </div>



        </div>
      </div>
      <div class='detail-close' @click='closeDetail'>
        <i class='icon-close'></i>
      </div>
    </div>   

  </div>
</template>

<script>
import star from '../star/star'
export default {
  props: {
    seller: {
      type: Object
    }
  },
  components: {
    star,
  },
  data() {
    return{
      detailShow: false
    }
  },
  methods: {
    showDetail() {
      this.detailShow = true;
    },
    closeDetail() {
      this.detailShow = false;
    }
  },
  created() {
    this.classMap=['decrease','discount','special','invoice','guarantee'];
  }

}

</script>
<style lang='stylus' rel='stylesheet/stylus'>
  @import '../../common/stylus/mixin.styl'

  .header
    color: #fff
    background: #999
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        font-size: 14px
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            width: 30px
            height: 18px
            font-size: 14px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
            vertical-align: top
          .name
            margin-left: 6px
            font-size: 16px
            font-weight: bold
            line-height: 18px
        .description
          margin-bottom: 10px
          font-size: 12px
          line-height: 12px
        .support
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            line-height: 16px
            font-size: 12px
      .support-count
        position: absolute
        right: 12px
        bottom: 14px
        padding: 0 8px
        height: 24px
        border-radius: 14px
        background: rgba(0,0,0,0.2)
        text-align: center
        line-height: 24px       
        .count
          vertical-alian: top
          font-size: 10px
        .icon-keyboard_arrow_right
          margin-left: 2px
          font-size: 10px
    .bulletin-wrapper
      position: relative
      height: 28px
      line-height: 28px
      padding: 0 12px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      background: rgba(7, 17, 27, .2)

      .bulletin-title
        display: inline-block
        width: 22px
        height: 12px
        bg-image('bulletin') 
        background-size: 12px 22px
        background-repeat: no-repeat
      .bulletin-text
        margin: 0 4px
        font-size: 10px
      .icon-keyboard_arrow_right
        position: absolute
        font-size: 10px
        right: 12px
        top: 8px
    .detail
      position: fixed
      width: 100%
      height: 100%
      overflow: auto
      z-index: 100
      top: 0
      left: 0
      background-color:rgba(7,17,27,0.8) 
      /*transition: all 0.5s 
        backdrop-filter: blur(10px)
      &.fade-transition 
        opacity: 1 
        background-color:rgba(7,17,27,0.8)  
      &.fade-enter,&.fade-leave 
        opacity: 0 
        background-color: rgba(7,17,27,0)*/
      .detail-wrapper
        width: 100%
        min-height: 100%
        .detail-main
          padding-top: 64px
          padding-bottom: 64px
          .name
            text-align: center
            font-size: 16px
            font-weight: 700
          .star-wrapper
            text-align: center
            margin-top: 18px
          .title
            display: flex
            width: 80%
            margin: 28px auto 24px auto
            .line
              flex: 1
              border-bottom: 1px solid rgba(255,255,255,0.2)
              position: relative 
              top: -6px
            .text
              padding: 0 12px 
              font-weight: 700
              font-size: 14px
          .supports
            margin: 0px auto 
            width: 80%    
            .support-item 
              padding: 0 12px 
              font-size: 0
              margin-bottom: 12px 
              & :last-child 
                margin-bottom: 0  
              .icon 
                vertical-align: top
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.guarantee
                  bg-image('guarantee_2')
                &.invoice
                  bg-image('invoice_2')
                &.special
                  bg-image('special_2')
                margin-right: 6px
                display: inline-block 
                width: 16px 
                height: 16px 
                background-size: 16px 16px 
                background-repeat: no-repeat
              .text 
                font-size: 14px
          .bulletin
            width: 80% 
            margin: 0 auto 
            .content 
              font-size: 12px
              line-height: 24px 
              padding: 0 12px
              

      .detail-close
        position: relative
        margin: -64px auto 0 auto
        width: 32px
        height: 32px
        clear: both
      
    

</style>