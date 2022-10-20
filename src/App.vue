<template>
  <HeaderBar />
  
  <div id="container" class="innerWrap">
    <LocationNavBar
      :lnbActive="lnbActive"
      @lnbToggle="lnbToggle()"
    />

    <ContentsWrap 
      :postList="postList"
      :rankSortingList="rankSortingList"
      :tabMenu="tabMenu"
      :class="{'extexsion': contWrapFolding}"
    />

  </div>

  <FooterBar />
</template>

<script>

import postList from './assets/post.js'
import HeaderBar from './components/Header.vue'
import LocationNavBar from './components/Lnb.vue'
import ContentsWrap from './components/Contents.vue'
import FooterBar from './components/Footer.vue'

export default {
  name: 'App',
  data() {
    return {
      lnbActive: true, // 사이드메뉴 상태
      contWrapFolding: false, // 콘텐츠 영역 상태
      tabMenu : ['spriteImg-txt_tabTitle_blog', 'spriteImg-txt_tabTitle_story'], // 콘텐츠 탭 메뉴
      postList: postList, // 인기블로그 데이터 js
      rankSortingList : [],
    }
  },
  methods: {
    lnbToggle() {
      this.lnbActive = !this.lnbActive
    },
  },
  mounted () {
    this.rankSortingList = this.postList.sort(function(a, b){
      return b.starPoint - a.starPoint
    });
  },
  components: {
    HeaderBar : HeaderBar, // 헤더
    LocationNavBar : LocationNavBar, // 사이드 메뉴
    ContentsWrap: ContentsWrap, // 콘텐츠영역
    FooterBar: FooterBar, // 푸터
  }
}
</script>

<style>

  @import url('./assets/reset.css');
  @import url('./assets/sprite.css');

  #app {
    background-color: #ccc;
  }

  #container{
    width: 1280px;
    margin: 0 auto;
    display: flex;
    position: relative;
    background-color: #f9f9f9;
    overflow: hidden;
  }

  @media screen and (max-width: 1280px) {
    #container,
    #contents{
      width: 100%;
    }
  }
</style>
