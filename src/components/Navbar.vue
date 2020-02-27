<template>
  <div class="navbar w-full z-10 bg-white">
    <div class="px-10 mx-auto flex items-center py-6 justify-between">
      <div class="font-sans font-bold">LOGO</div>
      <BurgerMenu />
    </div>
  </div>
</template>

<script>
import BurgerMenu from '@/components/BurgerMenu'

export default {
  components: {
    BurgerMenu
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  position: fixed;
  top: 0;
}
</style>