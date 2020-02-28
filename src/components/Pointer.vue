<template>
  <div class="pointer bg-tRed" ref="pointer"></div>
</template>

<script>
import { TweenLite } from 'gsap'

export default {
  mounted() {
    this.attachEvents()
  },  
  methods: {
    attachEvents() {
      let that = this
      window.addEventListener('mousemove', evt => {
        let pos = {
          x: evt.clientX,
          y: evt.clientY
        }
        let pointerWidth = 20
        TweenLite.to(this.$refs.pointer, 1, {
          x: pos.x - (pointerWidth / 2),
          y: pos.y - (pointerWidth / 2),
          scale: 1,
          onComplete() {
            TweenLite.to(that.$refs.pointer, .5, {
              scale: 1.5
            })
          }
        })
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../node_modules/mymixins/index';
.pointer {
  @include size(20px, 20px);
  border-radius: 50%;
  position: absolute;
  top: 0;
  left: 0;
}
</style>