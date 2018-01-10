<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>
<script>
    import Vue from 'vue'
    export default {
      props: {
        food: {
          type: Object
        }
      },
      methods: {
        addCart (event) {
          if (!this.food.count) {
            Vue.set(this.food, 'count', 1)
          } else {
            this.food.count ++
          }
          this.$root.eventHub.$emit('cart.add', event.target)
        },
        decreaseCart () {
          if (this.food.count) {
            this.food.count --
          }
        }
      }
    }
</script>
<style scoped lang="stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      .inner
        height: 24px
        line-height: 24px
        font-size: 24px
        color: rgb(0,160,220)
      /* 可以设置不同的进入和离开动画 */
      /* 设置持续时间和动画函数 */
    .move-enter-active
      transition: all .3s ease;
    .move-leave-active
      transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    .move-enter, .move-leave-to
      transform: translateX(10px);
      opacity: 0;

    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147,153,159)
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)
</style>
