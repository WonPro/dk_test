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
      <section id="bestSection">
        <h2 class="secTitle spriteImg spriteImg-txt_h2_best">
          <span class="hide">BEST</span>
        </h2>
        <div class="bestStoryWrap">
          <article class="mainStory">
            <figure>
              <img class="img" :style="{backgroundImage: 'url(' + postList[0].storyImg + ')'}" alt="">
              <figcaption> 
                <p class="title">
                  {{ postList[0].title }} 
                </p>
              </figcaption>
            </figure>
          </article>

          <article class="subStory">
            <figure 
              v-for="(item, i) in postList.slice(1, 5)"
              :key="i"
            >
              <img class="img" :style="{backgroundImage: 'url(' + item.storyImg + ')'}" alt="">
              <figcaption> 
                <p class="title">
                  {{ item.title }} 
                </p>
              </figcaption>
            </figure>
          </article>
        </div>
      </section>

      <section id="rankNewSection">
        <article class="ranking">
          <h2 class="secTitle spriteImg spriteImg-txt_h2_ranking">
            <span class="hide">RANKING</span>
          </h2>
          <ul class="rankList">
            <li
              v-for="(item, i) in rankSortingList.slice(0, 5)"
              :key="i"
              class="rankListItem"
            >
              <a href="" class="listTitle">{{ item.title }}</a>
              <div class="pointWrap">
                <span class="starPoint"></span>
                <span 
                  class="starPoint2"
                  :style="{width: item.starPoint*20 + '%'}"
                ></span>
              </div>
            </li>
          </ul>
        </article>

        <article class="new">
          <h2 class="secTitle spriteImg spriteImg-txt_h2_new">
            <span class="hide">NEW</span>
          </h2>
        </article>
      </section>
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
      rankSortingList: Array,
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

  #hotStory .bestStoryWrap{
    margin-top: 15px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  #hotStory .bestStoryWrap article{
    width: calc(50% - 0.5px);
  }

  #hotStory .bestStoryWrap .subStory{
    display: flex;
    flex-wrap: wrap;
    gap: 1px;
  }

  #hotStory .bestStoryWrap figure{
    position: relative;
  }

  #hotStory .bestStoryWrap .subStory figure{
    width: calc(50% - 2px);
  }

  #hotStory .bestStoryWrap .img{
    width: 100%;
    height: 0;
    padding-top: 73.12775330%;
    background-size: cover;
  }

  #hotStory .bestStoryWrap figure figcaption{
    position: absolute;
    bottom: 0;
    background-color: rgba(0,0,0,0.6);
  }

  #hotStory .bestStoryWrap .mainStory figcaption{
    padding: 29px;
  }

  #hotStory .bestStoryWrap .subStory figcaption{
    padding: 13px 15px;
  }

  #hotStory .bestStoryWrap figcaption .title{
    display: -webkit-box;
    color: #fff;
    line-height: 1.2;
    letter-spacing: -1px;
    overflow: hidden;
    text-overflow: ellipsis;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }

  #hotStory .bestStoryWrap .mainStory figcaption .title{
    padding-right: 100px;
    font-size: 20px;
  }

  #hotStory .bestStoryWrap .subStory figcaption .title{
    padding-right: 26px;
    font-size: 12px;
  }

  #hotStory #rankNewSection{
    margin-top: 60px;
    display: flex;
    gap: 1px;
  }

  #hotStory #rankNewSection article{
    width: calc(50% - 0.5px);
  }

  #hotStory #rankNewSection .pointWrap{
    width: 80px;
    position: relative;
  }

  #hotStory #rankNewSection .ranking .rankList{
    margin-top: 11px;
  }

  #hotStory #rankNewSection .ranking .rankList .rankListItem{
    padding: 10px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: nowrap;
    background-color: #fff;
    border-bottom: 1px solid #eee;
  }
  #hotStory #rankNewSection .ranking .rankList .rankListItem .listTitle{
    width: calc(100% - 90px);
    font-size: 14px;
    font-weight: bold;
    color: #000;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .starPoint{
    width: 100%;
    height: 13px;
    position: absolute;
    top: 0;
    left: 0;
    background: url(../assets/img_starRating1.png);
  }
  .starPoint2 {
    height: 13px;
    position: absolute;
    top: 0;
    left: 0;
    background: url(../assets/img_starRating2.png);
  }

</style>