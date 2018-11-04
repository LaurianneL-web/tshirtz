<template>
  <div id="app">
    <header>
      <div id="logo"><img src="./assets/img/logo.png" alt="TeeShirtz logo"></div>
      <div id="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
        <router-link to="/t-shirtz">T-shirtz</router-link>
      </div>
    </header>
      <router-view/>
    <footer-part></footer-part>
  </div>
</template>

<script>
import footerPart from "@/views/partial/Footer.vue";
  export default {
    components: {
      footerPart
    }
  }
</script>

<style lang="scss">
@import "./assets/styles/reset.scss";
@import "./assets/styles/layout.scss";
#app {
  font-family: $base_font;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
}
#nav {
  height: $nav_height;
  a {
    font-family: $title_font;
    font-size: 18px;
    color: $black;
    display: inline-block;
    text-decoration: none;
    height: $nav_height;
    width: 100px;
    line-height: $nav_height;
    transition: .5s transform;
    &:hover {
      background: $bleu;
      color: $white;
      transform: scale(1.2)
    }
  }
}
header{
  width: 100%;
  position: fixed;
  background: #fff;
      box-shadow: 0 0 15px rgba(0,0,0,.08), 0 0 4px rgba(0,0,0,.45);
  border-bottom: 3px solid $bleu !important;
  z-index: 4;
  #logo{
    float: left;
    height: $nav_height;
    > img{
      height: $nav_height;
    }
  }
}
h1{
  span{
    font-family: 'Pacifico', cursive;
    font-size: 46px;
  }
}
</style>
