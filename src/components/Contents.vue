<template>
  <div id="contentsWrap">
    <h2 class="sprite-txt sprite-txt_contTitle">
      <span class="hide">인기 카테고리</span>
    </h2>

    <div class="tabMenu">
      <button type="button" class="tabBtn on">
        <i class="sprite-txt sprite-txt_tabTitle_blog"></i>
      </button>
      <button type="button" class="tabBtn">
        <i class="sprite-txt sprite-txt_tabTitle_story"></i>
      </button>
    </div>

    <div class="viewCont">
      <div class="card">
        <div class="thumbnail"></div>
        <p class="cardTitle"></p>
        <div class="contInfo">
          <span class="source">{{ post.title }}</span>
          <span class="writter">{{ post.writter }}</span>
        </div>
        <div class="tagWrap">
          <div v-for="(tagList, i) in post.tags" :key="i" :class="tagList.color">{{ tagList.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'ContentsWrap',
    props: {

    }
  }
</script>

<style>
  #contentsWrap {
    width: 100%;
    padding: 46px 60px 60px 37px;
  }

  .tabMenu{
    width: 100%;
    margin-top: 22px;
    display: flex;
    justify-content: center;
  }

  .tabMenu .tabBtn{
    width: 50%;
    padding-top: 17px;
    padding-bottom: 17px;
    display: flex;
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

  .viewCont{
    padding: 11px 20px 19px 19px;
    background-color: #fbfbfb;
    border: 1px solid #a6a8ab;
    border-top: none;
  }

</style>