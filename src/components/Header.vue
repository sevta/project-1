<template>
  <div class="header-a">
    <Slider />
  </div>
</template>

<script>
import Slider from '@/components/Slider'

export default {
  components: {
    Slider
  }
}
</script>

<style lang="scss">
.header-a {
  position: relative;
  width: 100%;
  height: auto;
  background-color: white;
}
</style>