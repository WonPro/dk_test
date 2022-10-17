<template>
  <HeaderBar />
  
  <div id="contents" class="innerWrap">
    <LocationNavBar />
  </div>
</template>

<script>
import HeaderBar from './components/Header.vue'
import LocationNavBar from './components/Lnb.vue'

export default {
  name: 'App',
  data() {
    return {

    }
  },
  methods: {

  },
  components: {
    HeaderBar : HeaderBar,
    LocationNavBar : LocationNavBar,
  }
}
</script>

<style>

  @import url('./assets/reset.css');
  @import url('./assets/txt_sprite.css');

  #app {
    background-color: #ccc;
  }

  #contents{
    width: 1280px;
    min-height: calc(100vh - 65px);
    margin: 0 auto;
    position: relative;
  }
</style>
