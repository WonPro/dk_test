<template>
  <HeaderBar />
  
  <div id="container" class="innerWrap">
    <LocationNavBar :lnbActive="lnbActive" :lnbBtnState="lnbBtnState" @lnbToggle="lnbToggle()" />
    <ContentsWrap :class="{'extexsion': contWrapFolding}" />
  </div>
</template>

<script>
import HeaderBar from './components/Header.vue'
import LocationNavBar from './components/Lnb.vue'
import ContentsWrap from './components/Contents.vue'
import postList from './assets/post.js'

export default {
  name: 'App',
  data() {
    return {
      lnbActive: true,
      contWrapFolding: false,
      postList: postList,
    }
  },
  methods: {
    lnbToggle() {
      this.lnbActive = !this.lnbActive
    }
  },
  components: {
    HeaderBar : HeaderBar,
    LocationNavBar : LocationNavBar,
    ContentsWrap: ContentsWrap,
  }
}
</script>

<style>

  @import url('./assets/reset.css');
  @import url('./assets/txt_sprite.css');

  #app {
    background-color: #ccc;
  }

  #container{
    width: 1280px;
    min-height: calc(100vh - 65px);
    margin: 0 auto;
    display: flex;
    position: relative;
    overflow: hidden;
    background-color: #f9f9f9;
  }

  @media screen and (max-width: 1280px) {
    #contents{
      width: 100%;
    }
  }
</style>
