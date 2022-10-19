<template>
  <footer class="footer">
    <div class="innerWrap">
      <small class="copyright">Copyright (c) dk techin All rights reserved.</small>
    </div>
  </footer>
</template>

<script>
  export default {
    name: 'FooterBar',
  }
</script>

<style>
  .footer{
    width: 1280px;
    margin: 0 auto;
    padding-top: 18px;
    padding-bottom: 18px;
    background-color: #f1f1f1;
    text-align: center;
  }

  .footer .copyright{
    font-size: 13px;
    color: #777;
    letter-spacing: 0;
  }

  @media screen and (max-width: 1280px) {
    .footer{
      width: 100%;
    }
  }
</style>