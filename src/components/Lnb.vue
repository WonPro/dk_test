<template>
  <aside id="lnb">
    <ul class="lnb1Dep">
      <li class="current">
        <a href="" class="sprite-txt sprite-txt_h1_category" title="인기 카테고리"></a>
        <ul class="lnb2Dep">
          <li class="current">
            <a href="" class="sprite-txt sprite-txt_h2_blog" title="인기 블로그"></a>
          </li>
          <li>
            <a href="" class="sprite-txt sprite-txt_h2_story" title="인기 스토리"></a>
          </li>
        </ul>
      </li>
      <li>
        <a href="" class="sprite-txt sprite-txt_h1_tag" title="태그"></a>
        <ul class="lnb2Dep">
          <li class="current">
            <a href="" class="sprite-txt sprite-txt_h2_tag01" title="친절한답글러"></a>
          </li>
          <li>
            <a href="" class="sprite-txt sprite-txt_h2_tag02" title="해외여행"></a>
          </li>
          <li>
            <a href="" class="sprite-txt sprite-txt_h2_tag03" title="12월이슈포스트"></a>
          </li>
          <li>
            <a href="" class="sprite-txt sprite-txt_h2_tag04" title="100만구독"></a>
          </li>
        </ul>
      </li>
    </ul>
    <button type="button" id="lnbToggleBtn">
      <i class="icon_sprite sprite-icon_arrow-left"></i>
    </button>
  </aside>
</template>

<script>

export default {
  name: 'LocationNavBar'
}
</script>
<style>
  #lnb{
    width: 240px;
    min-height: -webkit-calc(100vh - 65px);
    min-height: -moz-calc(100vh - 65px);
    min-height: calc(100vh - 65px);
    position: fixed;
    top: 65px;
    left: calc(50% - 640px);
    border-right: 1px solid #ccc;
    padding-top: 110px;
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
    border: none;
    border-radius: 0 10px 10px 0;
    cursor: pointer;
  }
</style>