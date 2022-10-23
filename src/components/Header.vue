<template>
  <header class="header">
    <div class="innerWrap">
      <a href="" class="spriteImg spriteImg-txt_logo">
        <span class="hide">디케이테크인</span>
      </a>
    </div>
  </header>
</template>

<script>
  export default {
    name: 'HeaderBar',
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

  @media screen and (max-width: 1280px) {
    .header{
      width: 100%;
      padding: 34px 30px;
    }
  }
</style>