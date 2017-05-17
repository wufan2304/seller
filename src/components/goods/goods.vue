<template>
  <div class="goods">
    <div class="menu-wrapper" v-el:menu-wrapper>
      <ul>
        <li class="menu-item" v-for="item in goods">
          <span class="text">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" v-el:foods-wrapper>
      <ul>
        <li v-for="item in goods" class="food-list">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img width="57px" height="57px" :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span>
                  <span>好评率 {{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">¥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">¥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>

        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
  const ERR_OK = 0;
  export default{
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        goods: []
      };
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];

      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        if (response.error === ERR_OK) {
          this.goods = response.data;
          this.$nextTick(() => {
            this._initScroll();
          });
//              console.log(this.goods);
        }
      });
    },
    methods: {
        _initScroll() {
          this.menuScroll = new BScroll(this.$els.menuWrapper, {});
          this.foodsScroll = new BScroll(this.$els.foodsWrapper, {});
        }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl";
  .goods
    display: flex
    width: 100%
    position: absolute
    top: 174px
    bottom: 46px
    overflow: hidden
    .menu-wrapper
      flex: 0 0 80px
      width: 80px
      background-color: #f3f5f7
      .menu-item
        height: 54px
        width: 56px
        line-height: 14px
        margin: 0 auto
        display: table
        border-1px(rgba(7, 17, 27, 0.2))
        .icon
          display: inline-block
          width: 12px
          height: 12px
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
          vertical-align: middle
          font-size: 12px
    .foods-wrapper
      flex: 1
      .food-list
        .title
          font-size: 12px
          line-height: 26px
          color: rgb(147, 153, 159)
          padding-left: 14px
          height: 26px
          background-color: #f3f5f7
          border-left: 3px solid #d9dde1
        .food-item
          display: flex
          margin: 18px
          padding-bottom: 18px
          border-bottom: 1px solid rgba(7, 17, 27, 0.1)
          &:last-child
            margin-bottom: 0
          .icon
            flex: 0 0 57px
            margin-right: 10px
          .content
            .name
              margin: 2px 0 8px 0
              height: 14px
              line-height: 14px
              font-size: 14px
              color: rgb(7, 17, 27)
            .desc
              margin-bottom: 8px
              font-size: 10px
              line-height: 12px
              color: rgb(147,153,159)
            .extra
              line-height: 10px
              font-size: 10px
              color: rgb(147,153,159)
              .count
                margin-right: 12px
            .price
              font-weight: 700
              line-height: 24px
              .now
                margin-right: 8px
                font-size: 14px
                color: rgb(240,20,20)
              .old
                text-decoration: line-through
                font-size: 10px
                color: rgb(147,153,159)
</style>
