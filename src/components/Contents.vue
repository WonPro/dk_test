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
        <img
          class="thumbnail" 
          :src="post.image"
        >
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
              :class="tagList.tagClass != null ? tagList.tagClass : ''"
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
              <div class="img" :style="{backgroundImage: 'url(' + item.storyImg + ')'}"></div>
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
              <span class="listIndex">{{i + 1}}</span>
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
          <div class="contentsWrap">
            <div id="slider1">
              <h3 class="contTitle">#국내여행 블로그</h3>
              <Splide :options="options1">
                <SplideSlide v-for="(item, i) in postList" :key="i">
                  <div class="img" style="height: 48px;" :style="{background: 'url('+ item.slideThumbnail +') center center / cover no-repeat'}"></div>
                </SplideSlide>
              </Splide>
            </div>
            <div id="slider2">
              <h3 class="contTitle">#100만방문자</h3>
              <Splide :options="options2">
                <SplideSlide v-for="(item, i) in postList" :key="i">
                  <span class="img" style="width: 66px; height: 48px;" :style="{background: 'url('+ item.slideThumbnail +') center center / cover no-repeat'}"></span>
                  <span class="title">{{item.title}}</span>
                </SplideSlide>
              </Splide>
            </div>
          </div>
        </article>
      </section>
      <section id="adBanner">
        <div id="slider3">
          <Splide :options="options3">
            <SplideSlide v-for="(item, i) in 5" :key="i">
              <div style="height: 0; padding-top: 43.2432432%; background: url(./img_slide.png) center center / contain no-repeat; display: block;"></div>
            </SplideSlide>
          </Splide>
        </div>
      </section>
    </div>

  </div>
</template>

<script>
import { Splide, SplideSlide } from '@splidejs/vue-splide';
import '@splidejs/vue-splide/css';


  export default {
    name: 'ContentsWrap',
    data() {
      return {
        currentTab: 0, // 현재 선택한 탭의 Index
        hotViews: 1000, // Hot 아이콘 획득 조회수 기준
        nowDate: '', // 오늘 년월일
        recentDate: '', // 7일 전 년월일
        options1: {
          type   : 'slide',
          perPage: 5,
          perMove: 1,
          gap: 10,
          arrows: true,
          drag: false,
          pagination: false,
        },
        options2: {
          type   : 'slide',
          perPage: 2,
          perMove: 1,
          gap: 10,
          arrows: true,
          drag: false,
          pagination: false,
        },
        options3: {
          type   : 'loop',
          rewind: false,
          perPage: 1.3,
          perMove: 1,
          gap: 20,
          clones: 1,
          focus: 'center',
          drag: false,
          pagination: false,
        },
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
    components: {
      Splide,
      SplideSlide,
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
    border: 1px solid #c6cbce;
    border-top: none;
  }

  .viewCont.on{
    display: block;
  }

  @media screen and (max-width: 640px) {
    #contentsWrap {
      height: calc(100vh - 146px);
      padding: 0;
    }

    #lnbWrap.active + #contentsWrap {
      width: 100%;
    }

    .viewCont{
      padding: 15px 0;
    }

    .spriteImg-txt_contTitle{
      margin-top: 42px;
      margin-left: 30px;
    }
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

  #hotBlog .card .thumbnail{
    width: 240px;
    height: 176px;
    display: block;
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
    background-color: #b3b6bb;
    -webkit-border-radius: 2px; -moz-border-radius: 2px;
    border-radius: 2px;
    font-size: 14px;
    font-weight: bold;
    color: #fff;
  }

  #hotBlog .card .cardCont .tag.green{background-color: #86bbb2;}
  #hotBlog .card .cardCont .tag.blue{background-color: #9da3d7;}
  #hotBlog .card .cardCont .tag.yello{background-color: #ccc76c;}
  #hotBlog .card .cardCont .tag.red{background-color: #a37a7b;}

  @media screen and (max-width: 640px) {
    #hotBlog .card .thumbnail{
      display: none;
    }

    #hotBlog .card .cardCont{
      width: 100%;
      padding: 40px 34px 40px 30px;
    }

    #hotBlog .card .cardCont .cardTitle{
      padding-right: 0;
      line-height: 1.4;
      white-space: unset;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
    }

    #hotBlog .card .cardCont .cardTitle.new:after,
    #hotBlog .card .cardCont .cardTitle.hot:after{
      position: static;
      display: inline-block;
      margin-left: 5px;
    }

    #hotBlog .card .cardCont .contInfo{
      margin-top: 15px;
    }

    #hotBlog .card .cardCont .tagWrap{
      margin-top: 20px;
    }

    #hotBlog .card .cardCont .tag{padding: 0; background-color: transparent; color: #b3b6bb;}
    #hotBlog .card .cardCont .tag.green{background-color: transparent; color: #86bbb2;}
    #hotBlog .card .cardCont .tag.blue{background-color: transparent; color: #9da3d7;}
    #hotBlog .card .cardCont .tag.yello{background-color: transparent; color: #ccc76c;}
    #hotBlog .card .cardCont .tag.red{background-color: transparent; color: #a37a7b;}
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
    justify-content: space-between;
    gap: 1px;
  }

  #hotStory #rankNewSection article{
    width: calc(50% - 5px);
  }

  #hotStory #rankNewSection .pointWrap{
    width: 82px;
    position: relative;
  }

  #hotStory #rankNewSection .ranking .rankList{
    margin-top: 15px;
  }

  #hotStory #rankNewSection .ranking .rankList .rankListItem{
    padding: 10px 10px 10px 0;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: nowrap;
    background-color: #fff;
    border-bottom: 1px solid #eee;
  }

  #hotStory #rankNewSection .ranking .rankList .rankListItem .listIndex{
    width: 24px;
    font-size: 14px;
    font-weight: bold;
    text-align: center;
  }

  #hotStory #rankNewSection .ranking .rankList .rankListItem .listTitle{
    width: calc(100% - 106px);
    font-size: 14px;
    font-weight: bold;
    color: #000;
    text-decoration: none;
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
    background: url(../assets/img_starRating1.png) left center / contain no-repeat;
  }
  .starPoint2 {
    height: 13px;
    position: absolute;
    top: 0;
    left: 0;
    background: url(../assets/img_starRating2.png) left center / cover no-repeat;
  }

  
  #rankNewSection .new .contentsWrap{
    margin-top: 15px;
    padding: 10px;
    background-color: #fff;
  }

  #rankNewSection .new .contentsWrap .contTitle{
    margin-bottom: 5px;
    font-weight: bold;
    color: #808080;
  }

  #rankNewSection .new #slider1 .img{
    height: 48px;
  }
  #rankNewSection .new #slider2{
    margin-top: 17px;
  }

  #rankNewSection .new #slider2 .img{
    width: 66px;
    height: 48px;
  }

  #rankNewSection .new #slider2 .title{
    width: calc(100% - 71px);
    display: -webkit-box;
    padding-right: 10px;
    word-break: keep-all;
    font-size: 12px;
    font-weight: bold;
    line-height: 1.4;
    overflow: hidden;
    text-overflow: ellipsis;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }

  #rankNewSection .new #slider2 .splide__slide{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .splide__track{
    padding-left: 0px;
    padding-right: 0px;
    width: 85%;
    margin: 0 auto;
  }

  .splide__arrow{
    background-color: transparent;
  }

  .splide__arrow--prev{
    left: 0;
  }

  .splide__arrow--next{
    right: 0;
  }

  .splide__arrow svg{
    fill: #bab8b8;
  }

  #slider3{
    margin-top: 80px;
  }

  #slider3 .splide__track{
    width: 100%;
  }

  #slider3 .splide__arrow--prev{
    left: 8rem;
  }

  #slider3 .splide__arrow--next{
    right: 8rem;
  }

  #slider3 .splide__arrow{
    width: 3rem;
    height: 3rem;
    background-color: rgba(0, 0, 0, 0.5);
  }

  #slider3 .splide__arrow svg{
    width: 25px;
    height: 25px;
    fill: #bab8b8;
  }

  @media screen and (max-width: 640px) {
    #hotStory{
      padding: 30px;
    }

    #hotStory #bestSection{
      margin-top: 10px;
    }

    #hotStory .bestStoryWrap article{
      width: 100%;
    }

    #hotStory .bestStoryWrap .subStory{
      margin-top: 2px;
    }

    #hotStory .bestStoryWrap .mainStory figcaption{
      padding: 10px;
    }
    
    #hotStory .bestStoryWrap .mainStory figcaption .title{
      padding-right: 0;
      font-size: 16px;
    }

    #hotStory .bestStoryWrap .subStory figure{
      width: calc(50% - 1px);
    }

    #hotStory .bestStoryWrap .subStory figcaption{
      padding: 6px;
    }

    #hotStory .bestStoryWrap .subStory figcaption .title{
      padding-right: 0;
      font-size: 12px;
    }

    #hotStory #rankNewSection{
      gap: 0;
      flex-wrap: wrap;
      margin-top: 40px;
    }

    #hotStory #rankNewSection article{
      width: 100%;
    }

    #hotStory #rankNewSection .ranking{
      order: 2;
      margin-top: 60px;
    }

    #hotStory #rankNewSection .new{
      order: 1;
    }

    #slider3 .splide__arrow--prev{
    left: 10%;
    }

    #slider3 .splide__arrow--next{
      right: 10%;
    }

  }
</style>