<template>
  <div id="app">
    <Header />
    <transition>
      <router-view />
    </transition>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header/Header.vue';
import Footer from './components/Footer/Footer.vue';

export default {
  name: 'app',
  components: {
    Header,
    Footer
  }
}
</script>

<style lang="scss" src="./scss/main.scss">
  #app {
    position: relative;
  }
</style>
