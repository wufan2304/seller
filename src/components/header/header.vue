<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <star :size="48" :score="seller.score"></star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text"></div>
            <div class="line"></div>
          </div>
          <div v-for="item in seller.supports" class="support">
            <span class="icon" :class="classMap[item.type]"></span>
            <span class="text">{{item.description}}</span>
          </div>
          <hr>
          <p class="bulletin">{{seller.bulletin}}</p>
        </div>
      </div>
      <div class="detail-close" @click="closeDetail">
        <i class="icon-close"></i>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star';
  export default {
    components: {
        star
    },
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      };
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
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl";
  @import "../../common/stylus/base.styl";
  .header
    background: rgba(7, 17, 27, 0.5)
    color: #fff
    position: relative
    overflow: hidden
    .content-wrapper
      padding: 24px 12px 18px 24px
      display: flex
      position: relative
      .avatar
        img
          border-radius: 2px
      .content
        margin-left: 16px
        font-size: 0
        .title
          display: flex
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            /*vertical-align: top*/
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            font-size: 16px
            line-height: 18px
            font-weight: bold
            margin-left: 6px
        .description
          margin-bottom: 10px
          font-size: 12px
          line-height: 12px
        .support
          font-size: 10px
          line-height: 12px
          display: flex
          .icon
            display: inline-block
            margin-right: 4px
            width: 12px
            height: 12px
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
            line-height: 12px
            font-size: 10px
      .support-count
        position: absolute
        right: 12px
        bottom: 18px
        background-color: rgba(0, 0, 0, 0.2)
        height: 24px
        border-radius: 12px
        display: flex
        align-items: center
        .count
          margin-left: 8px
          font-size: 10px
          line-height: 12px
          margin-right: 2px
        .icon-keyboard_arrow_right
          font-size: 10px
          margin-right: 8px

    .bulletin-wrapper
      height: 28px
      display: flex
      align-items: center
      padding: 0 12px 0 12px
      background: rgba(7, 17, 27, 0.2)
      .bulletin-title
        display: inline-block
        width: 22px
        height: 12px
        bg-image('bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
        margin-right: 4px
      .bulletin-text
        /*height: 28px*/
        white-space: nowrap
        display: inline-block
        overflow: hidden
        text-overflow: ellipsis
        line-height: 28px
        font-size: 10px
        margin-right: 4px
        flex: 1
      .icon-keyboard_arrow_right
        font-size: 10px

    .background
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)

    .detail
      position: fixed
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: 100
      overflow: auto
      background: rgba(7, 17, 27, 0.8)
      .detail-wrapper
        min-height: 100%
        width: 100%
        .detail-main
          margin: 64px 36px 0 36px
          padding-bottom: 64px
          .name
            line-height: 16px
            text-align: center
            font-size: 16px
            font-weight: 700
          .star-wrapper
            margin-top: 18px
            padding: 2px 0
            text-align: center
          .support
            margin: 24px 12px 28px 12px
            font-size: 12px
            line-height: 12px
            .icon
              display: inline-block
              margin-right: 4px
              width: 12px
              height: 12px
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

          .bulletin
            margin: 24px 12px 28px 12px
            line-height: 24px
            font-size: 12px
      .detail-close
        margin-top: -64px
        text-align: center
        font-size: 32px
</style>
