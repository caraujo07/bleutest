<template>
  <div id="app">
    <Header />
    <transition>
      <router-view />
    </transition>
  </div>
</template>

<script>
import Header from './components/Header/Header.vue';

export default {
  name: 'app',
  components: {
    Header
  }
}
</script>

<style lang="scss" src="./scss/main.scss"></style>
