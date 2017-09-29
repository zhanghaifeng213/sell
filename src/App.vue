<template>
  <div id="app">
    <vHeader :seller="seller"></vHeader>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link :to="{ path: '/goods' }">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ path: '/ratings' }">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ path: '/seller' }">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import vHeader from './components/header/header.vue';
  const ERR_OK = 0;
  export default {
    data() {
      return {
        seller: {
          type: Object
        }
      };
    },
    created() {
      this.$http.get('/api/seller').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = response.data;
        };
      });
    },
    components: {
      vHeader
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/base.styl"
  @import "./common/stylus/mixin.styl"
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    // border-bottom:1px solid rgba(7,17,27,0.1)
    border-1px(rgba(7,17,27,0.1))
  .tab-item
    flex: 1
    text-align: center
    & > a
      font-size: 14px
      color: rgb(77,85,93)
      &.active
        color: rgb(240,20,20)
</style>
