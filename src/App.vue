<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods" activeClass="active">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings" activeClass="active">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller" activeClass="active">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>
<script>
  import header from './components/header/header.vue'
  const ERR_OK = 0
  export default {
    name: 'app',
    data: function () {
      return {
        seller: {}
      }
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.seller = response.data
        }
      })
    },
    components: {
      'v-header': header
    }
  }
</script>
<style scoped lang="stylus">
  @import "./common/stylus/mixin.styl"
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height 40px
      border-1px(rgba(7, 17, 27, 0.1))
      .tab-item
        flex 1
        text-align center
        & > a
          display: block
          font-size 14px
          color: rgb(77, 85, 93)
          &.active
            color: rgb(240, 20, 20)
</style>
