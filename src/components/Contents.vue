<template>
  <div id="contentsWrap">
    <h2 class="spriteImg spriteImg-txt_contTitle">
      <span class="hide">인기 카테고리</span>
    </h2>

    <div class="tabMenu">
      <button type="button" class="tabBtn" 
        v-for="(tab, index) in tabMenu"
        :key="index"
        :class="{on: currentTab == index}" 
        @click="chosenTab(index)"
      >
        <i class="spriteImg" :class="tab"></i>
      </button>
    </div>

    <ul
      id="hotBlog"
      class="viewCont"
      :class="{on: currentTab == 0}"
    >
      <li 
        class="card"
        v-for="(post, i) in postList"
        :key="i"
      >
        <div
          class="thumbnail spriteImg" 
          :class="post.image"
        ></div>
        <div class="cardCont">
          <div class="wrapper">
            <!-- 블로그 제목, new, hot아이콘 생성 -->
            <a
              :href="post.link"
              class="cardTitle"
              :class="[
                post.date >= recentDate ? 'new' : '',
                post.views >= hotViews ? 'hot' : ''
              ]"
              target="_blank"
            >
              {{post.title}}
            </a><!-- 블로그 제목, new, hot아이콘 생성 -->
            <div class="contInfo">
              <span class="source">{{ post.source }}</span>
              <span class="writer">{{ post.writer }}</span>
            </div>
          </div>
          <div class="tagWrap">
            <!-- 태그 아이콘 생성 -->
            <span 
              v-for="tagList in post.tags"
              :key="tagList"
              class="tag" 
              :style="{backgroundColor : tagList.tagColor}"
            >
              {{ tagList.tagNm }}
            </span><!-- 태그 아이콘 생성 -->
          </div>
        </div>
      </li>
    </ul>

    <div id="hotStory" class="viewCont" :class="{on: currentTab == 1}">
      
    </div>
  </div>
</template>

<script>
  export default {
    name: 'ContentsWrap',
    data() {
      return {
        currentTab: 0, // 현재 선택한 탭의 Index
        hotViews: 1000, // Hot 아이콘 획득 조회수 기준
        nowDate: '', // 오늘 년월일
        recentDate: '', // 7일 전 년월일
      }
    },
    mounted () {

      // 매 초 마다 날짜 함수 받아옴
      this.nowDate = setInterval(() => {    
        this.setNowTimes()
      }, 1000)
    },
    methods: {

      // 클릭한 탭을 currentTab으로 저장
      chosenTab(i) {
        this.currentTab = i;
      },

      // 날짜 받기 함수
      setNowTimes () { 
        let myDate = new Date(),
            yy = myDate.getFullYear(),
            mm = myDate.getMonth() + 1,
            dd = myDate.getDate() < 10 ? '0' + myDate.getDate() : myDate.getDate(),
            d7 = myDate.getDate() - 7 < 10 ? '0' + myDate.getDate() - 7 : myDate.getDate() - 7;

        this.nowDate = yy + '-' + mm + '-' + dd;
        this.recentDate = yy + '-' + mm + '-' + d7;
      }
    },
    props: {
      tabMenu: Array,
      postList: Array,
    }
  }
</script>

<style>
  #contentsWrap {
    width: 100%;
    height: -webkit-calc(100vh - 117px);
    height: -moz-calc(100vh - 117px);
    height: calc(100vh - 117px);
    padding: 46px 34px 60px 37px;
    overflow-y: auto;
    -webkit-transition: width 0.3s; -moz-transition: width 0.3s; -o-transition: width 0.3s;
    transition: width 0.3s;
  }

  #lnbWrap.active + #contentsWrap{
    width: -webkit-calc(100% - 214px); width: -moz-calc(100% - 214px);
    width: calc(100% - 214px);
  }

  #contentsWrap::-webkit-scrollbar {
    width: 6px;
  }
  
  #contentsWrap::-webkit-scrollbar-track {
    background-color: #E6E6E6;
  }
  
  #contentsWrap::-webkit-scrollbar-thumb {
    background-color: #777;
    -webkit-border-radius: 3px; -moz-border-radius: 3px;
    border-radius: 3px;
  }

  .tabMenu{
    width: 100%;
    margin-top: 22px;
    display: -webkit-box; display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: center; -ms-flex-pack: center;
    justify-content: center;
  }

  .tabMenu .tabBtn{
    width: 50%;
    padding-top: 17px;
    padding-bottom: 17px;
    display: -webkit-box; display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: center; -ms-flex-pack: center;
    justify-content: center;
    align-items: center;
    background-color: #f3f3f5;
    border: 1px solid #c6cbce;
    border-top: 2px solid #a6a8ab;
    cursor: pointer;
  }

  .tabMenu .tabBtn.on{
    background-color: #fbfbfb;
    border-top: 2px solid #57595b;
    border-bottom: none;
  }

  .tabMenu .tabBtn:first-of-type{
    border-right: none;
  }

  .viewCont{
    display: none;
    padding: 14px 18px 18px 18px;
    background-color: #fbfbfb;
    border: 1px solid #a6a8ab;
    border-top: none;
  }

  .viewCont.on{
    display: block;
  }

  #hotBlog .card{
    display: -webkit-box; display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: start; -ms-flex-pack: start;
    justify-content: flex-start;
    margin-top: 11px;
    background-color: #fff;
    border-right: 2px solid #efeef2;
    border-bottom: 2px solid #efeef2;
  }
  
  #hotBlog .card:first-of-type{
    margin-top: 0;
  }

  #hotBlog .card .cardCont{
    width: -webkit-calc(100% - 240px); width: -moz-calc(100% - 240px);
    width: calc(100% - 240px);
    padding: 30px 40px 20px 38px;
    display: -webkit-box; display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical; -ms-flex-direction: column;
    flex-direction: column;
    -webkit-box-pack: justify; -ms-flex-pack: justify;
    justify-content: space-between;
  }

  #hotBlog .card .cardCont .cardTitle{
    max-width: 100%;
    display: inline-block;
    padding-right: 24px;
    position: relative;
    font-size: 20px;
    font-weight: bold;
    text-decoration: none;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    color: #223050;
  }

  #hotBlog .card .cardCont .cardTitle:hover{
    cursor: pointer;
    text-decoration: underline;
    color: #445272;
  }

  #hotBlog .card .cardCont .cardTitle.new:after{
    content: '';
    width: 16px;
    height: 16px;
    background-position: -83px -5px;
    background-image: url(../assets/spritesheet.png);
    background-repeat: no-repeat;
    display: block;
    position: absolute;
    right: 0;
    top: 2px;
  }

  #hotBlog .card .cardCont .cardTitle.hot:after{
    content: '';
    width: 16px;
    height: 16px;
    background-position: -57px -5px;
    background-image: url(../assets/spritesheet.png);
    background-repeat: no-repeat;
    display: block;
    position: absolute;
    right: 0;
    top: 2px;
  }

  #hotBlog .card .cardCont .contInfo{
    margin-top: 12px;
  }

  #hotBlog .card .cardCont .contInfo .source{
    margin-right: 21px;
    position: relative;
    font-size: 14px;
    color: #888;
  }

  #hotBlog .card .cardCont .contInfo .source:after{
    content: '';
    width: 1px;
    height: 14px;
    position: absolute;
    bottom: 2px;
    right: -11px;
    background-color: #bfbfbf;
  }

  #hotBlog .card .cardCont .contInfo .writer{
    font-size: 14px;
    color: #888;
  }

  #hotBlog .card .cardCont .tagWrap{
    display: -webkit-box; display: -ms-flexbox;
    display: flex;
    gap: 6px;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
  }

  #hotBlog .card .cardCont .tag{
    padding: 5px 10px;
    -webkit-border-radius: 2px; -moz-border-radius: 2px;
    border-radius: 2px;
    font-size: 14px;
    font-weight: bold;
    color: #fff;
  }

  #hotStory{
    padding: 17px;
  }

</style>