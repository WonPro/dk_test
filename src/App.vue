<template>
  <HeaderBar
    :lnbActive="lnbActive"
    @lnbToggle="lnbToggle()"
  />
  
  <div id="container" class="innerWrap">
    <LocationNavBar
      :lnbActive="lnbActive"
      @lnbToggle="lnbToggle()"
      @tabNumber="tabNumber"
    />

    <ContentsWrap 
      :postList="postList"
      :originData="originData"
      :rankSortingList="rankSortingList"
      :tabMenu="tabMenu"
      :currentTab="currentTab"
      :class="{'extexsion': contWrapFolding}"
      @tabNumber="tabNumber"
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
      currentTab : 0,
      postList: postList, // 정렬용 복제데이터
      rankSortingList : [...postList], // 별점순 정렬한 인기블로그 데이터
    }
  },
  methods: {
    // 사이드메뉴 토글
    lnbToggle() {
      this.lnbActive = !this.lnbActive
    },
  
    // 클릭한 탭을 currentTab으로 저장
    tabNumber(tabNumber) {
      this.currentTab = tabNumber;
    },
  },
  mounted () {
    this.rankSortingList = this.rankSortingList.sort(function(a, b){
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
