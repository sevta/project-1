<template>
  <div id="app">
    <Navbar />
    <Menu :show="menuOpen" />
    <Command v-if="showCommandLine" />
    <Pointer />
    <div class="scroll-container">
      <router-view/>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

import Menu from '@/components/Menu'
import Navbar from '@/components/Navbar'
import Command from '@/components/Command'
import Pointer from '@/components/Pointer'

import SmoothScrollbar from 'smooth-scrollbar'

export default {
  name: 'app',
  computed: {
    ...mapState([
      'menuOpen'
    ])
  },
  data: () => ({
    smoothScrollbarInstance: null,
    scrollY: 0,
    showMenu: false,
    showCommandLine: false
  }),
  components: {
    Menu,
    Command,
    Navbar,
    Pointer
  },
  mounted() {
    this.initSmoothScrollbar()
  },
  methods: {
    initSmoothScrollbar() {
      SmoothScrollbar.init(document.querySelector('.scroll-container'))
    }
  }
}
</script>

<style lang="scss">
body { overflow: hidden; }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  .scroll-container {
    width: 100%;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    // padding-top: 100px;
  }

  .content {
    height: 500vh;

    .header {
      position: relative;
      width: 100%;
      height: 100vh;
      background-color: deeppink;
      overflow: hidden;
      &-bg {
        width: 100%;
        height: 100%;
        background-image: url(https://images.unsplash.com/photo-1581864778188-450db0c9f0e6?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=632&q=80);
        background-repeat: no-repeat;
        background-position: center;
        background-size: 100%;
        position: absolute;
        top: 0;
        left: 0;
      }
    }
  }
}



</style>
