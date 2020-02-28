<template>
  <div class="burger-menu shadow-lg" @click="toggleMenu">
    <div class="burger-menu--inner bg-tRed text-white">
      <div class="text-sm font-bold font-sans z-10">Menu</div>
    </div>
    <!-- <span></span>
    <span></span>
    <span></span> -->
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  computed: {
    ...mapState([
      'menuOpen'
    ])
  },
  data: () => ({
    showMenu: false
  }),
  props: {
    onOpen: {
      type: Function
    }
  },
  methods: {
    toggleMenu() {
      this.showMenu = !this.showMenu
      this.$nextTick(() => {
        this.$store.commit('toggleMenu', this.showMenu)
        if (this.onOpen) this.onOpen(this.showMenu)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '../../node_modules/mymixins/index';

  .burger-menu {
    --menu-width: 55px;
    width: var(--menu-width);
    height: var(--menu-width);
    position: relative;
    // top: 40px;
    // right: 40px;
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    z-index: 5;
    cursor: pointer;
    &::before {
      content: '';
      @include size(99%, 99%);
      @include absolute-center();
      background-color: #222;
      z-index: 4;
    }
    &--inner {
      position: relative;
      @include size(100%, 100%);
      z-index: 6;
      @include flex-center();
      transition: all .3s ease;
      &:hover {
        transform: translate(6px, -6px);
      }
    }
    span {
      width: 100%;
      border-radius: 3px;
      height: 3px;
      background-color: #333;
    }
  }
</style>