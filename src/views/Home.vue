<template>
  <div class="home">
    <div>
      <img alt="TeeShirtz logo" src="../assets/img/logo.png">
      <h1>Premier site d'e-commerce où vous n'achetez absolument rien !</h1>
    </div>
  </div>
</template>

<script>

export default {
  name: 'home',
  components: {
  }
}
</script>

<style lang="scss" scoped>
.home{
  padding-top: 50px;
  div{
    width: 60%;
    height: 512px;
    box-shadow: 0px 0px 114px 0 rgba(0, 0, 0, 0.1);
    background-color: #fff;
    margin: 40px auto 30px auto;
    line-height: 36px;
    h1{
      background: #000;
      color: white;
    }
  }
}
</style>

