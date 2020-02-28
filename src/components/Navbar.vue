<template>
  <div class="navbar w-full z-10">
    <div class="px-5 md:px-10 mx-auto flex items-center py-6 justify-between">
      <div class="font-heading2 text-tBlack text-2xl border-1 border-black px-2 py-0">S.A SAPUTRA</div>
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
  transition: all .3s ease;
}
</style>