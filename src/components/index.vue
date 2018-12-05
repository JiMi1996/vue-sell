<template>
  <div class="app">
    <Header :seller="seller"></Header>
    <div class="tab">
      <div class="tab-item">
        <router-link class="link-item" to="/goods">食谱</router-link>
      </div>
      <div class="tab-item">
        <router-link class="link-item" to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link class="link-item" to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>

import Header from './header/header'

const ERROR_OK = 0

export default {
  name: 'index',
  components: {
    Header
  },
  data () {
    return {
      seller: {}
    }
  },
  created() {
    this.$http.get('/api/seller').then((res) => {
      res = res.body
      console.log(res)
      if (res.errno === ERROR_OK) {
        this.seller = res.data
        console.log(this.seller)
      }
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus">
  @import "../common/stylus/mixin.styl"
  .app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex: 1
        text-align: center
        .link-item
          display: block
          font-size: 14px
          color: rgb(77,85,93)
          &.active
            color: rgb(240,20,20)
</style>
