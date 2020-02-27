<template>
  <div class="about text-white font-sans bg-gray-900">
    <h1>This is an about page</h1>
  </div>
</template>

<script>
import Draggable from "gsap/Draggable"; 
import { TweenLite, TimelineMax, Linear, Back, Sine } from 'gsap'
export default {
  name: 'about',
  data: () => ({
    timline: new TweenLite()
  }),
  methods: {
    checkHit(a, b) {
      return Draggable.hitTest(a, b)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../node_modules/mymixins/index';

.container-games {
  position: relative;
  width: 600px;
  height: 600px;
  background-color: whitesmoke;
  margin: 0 auto;
  .box {
    width: 60px;
    height: 60px;
    background-color: deeppink;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-weight: bold;
  }
  .box-b {
    width: 120px;
    height: 20px;
    background-color: teal;
    position: absolute;
    bottom: 0;
    left: 0;
  }
}
</style>