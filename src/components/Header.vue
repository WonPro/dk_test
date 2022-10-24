<template>
  <header class="header">
    <div class="innerWrap">
      <a href="" class="spriteImg spriteImg-txt_logo">
        <span class="hide">디케이테크인</span>
      </a>
      <button type="button" class="mobileGnb" @click="closeLnb">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>
  </header>
</template>

<script>
  export default {
    name: 'HeaderBar',
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
  .header{
    width: 1280px;
    margin: 0 auto;
    padding-top: 20px;
    padding-bottom: 20px;
    background-color: #fff;
    border-bottom: 1px solid #ccc;
  }

  .header .innerWrap{
    display: flex;
    justify-content: space-between;
  }

  .mobileGnb{
    display: none;
  }

  @media screen and (max-width: 1280px) {
    .header{
      width: 100%;
      padding: 34px 30px;
    }

    .mobileGnb{
      width: 52px;
      padding: 0;
      display: block;
      background-color: transparent;
      border: none;
    }

    .mobileGnb span{
      width: 100%;
      height: 4px;
      display: block;
      border-radius: 2px;
      background-color: #000;
    }

    .mobileGnb span:nth-child(2){
      margin: 8px 0;
      background-color: #ffb738;
    }
  }
</style>