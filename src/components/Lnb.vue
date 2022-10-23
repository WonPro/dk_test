<template>
  <aside id="lnbWrap" :class="{active: lnbActive}">
    <nav id="lnb">
      <ul class="lnb1Dep">
        <li class="current">
          <a href="" class="spriteImg spriteImg-txt_h1_category" title="인기 카테고리"></a>
          <ul class="lnb2Dep">
            <li class="current">
              <a href="" class="spriteImg spriteImg-txt_h2_blog" title="인기 블로그"></a>
            </li>
            <li>
              <a href="" class="spriteImg spriteImg-txt_h2_story" title="인기 스토리"></a>
            </li>
          </ul>
        </li>
        <li>
          <a href="" class="spriteImg spriteImg-txt_h1_tag" title="태그"></a>
          <ul class="lnb2Dep">
            <li class="current">
              <a href="" class="spriteImg spriteImg-txt_h2_tag01" title="친절한답글러"></a>
            </li>
            <li>
              <a href="" class="spriteImg spriteImg-txt_h2_tag02" title="해외여행"></a>
            </li>
            <li>
              <a href="" class="spriteImg spriteImg-txt_h2_tag03" title="12월이슈포스트"></a>
            </li>
            <li>
              <a href="" class="spriteImg spriteImg-txt_h2_tag04" title="100만구독"></a>
            </li>
          </ul>
        </li>
      </ul>
    </nav>
    <button type="button" id="lnbToggleBtn" @click="closeLnb">
      <i class="spriteImg" :class="{'spriteImg-icon_arrow-left': lnbActive, 'spriteImg-icon_arrow-right' : !lnbActive}"></i>
      <span class="hide">{{ lnbActive ? '메뉴 닫기' : '메뉴 열기' }}</span>
    </button>
  </aside>
</template>

<script>

export default {
  name: 'LocationNavBar',
  methods: {
    closeLnb() {
      this.$emit('lnbToggle')
    }
  },
  props: {
    active: String,
    lnbActive: Boolean
  }
}
</script>
<style>

  #lnbWrap{
    width: 240px;
    margin-left: -266px;
    position: relative;
    -webkit-transition: margin-left 0.3s;
    -moz-transition: margin-left 0.3s;
    -o-transition: margin-left 0.3s;
    transition: margin-left 0.3s;
  }
  
  #lnbWrap.active{
    margin-left: -26px;
  }

  #lnb{
    height: -webkit-calc(100vh - 117px);
    height: -moz-calc(100vh - 117px);
    height: calc(100vh - 117px);
    border-right: 1px solid #ccc;
    padding-top: 47px;
    padding-left: 26px;
    background-color: #fff;
  }

  #lnb.on{
    left: 240px;
  }

  .lnb1Dep li{
    margin-top: 67px;
  }

  .lnb1Dep li:first-child{
    margin-top: 0;
  }

  .lnb2Dep{
    margin-top: 21px;
    padding-left: 10px;
  }

  .lnb2Dep li{
    margin-top: 14px;
  }

  .lnb2Dep li:first-child{
    margin-top: 0;
  }

  #lnbToggleBtn{
    width: 28px;
    height: 300px;
    position: absolute;
    top: 99px;
    right: -28px;
    background-color: #ffcc56;
    border: 1px solid #f8bb4f;
    -webkit-border-radius: 0 10px 10px 0;
    -moz-border-radius: 0 10px 10px 0;
    border-radius: 0 10px 10px 0;
    box-shadow: 0 2px 3px rgba(0,0,0,0.26);
    cursor: pointer;
  }

  @media screen and (max-width: 640px) {
    #lnbWrap {
      position: fixed;
      left: -240px;
    }
  }

</style>