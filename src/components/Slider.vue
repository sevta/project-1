<template>
  <div class="homepage-slider-container">
    <div class="homepage-slider font-sans">
      <div class="homepage-slider--inner">
        <transition name='fadeUp'>
          <div class="homepage-slider--label text-yellow-600 text-shadow font-bold" v-if="animateToggle">{{ label }}</div>
        </transition>
        <div class="homepage-slider--img">
          <transition
            v-on:before-enter="beforeEnter"
            v-on:enter="enter"
            v-on:before-leave="beforeLeave"
            v-on:leave="leave"
          >
            <div class="img-container shadow bg-gray-700" v-if="animateToggle">
              <div class="back-layer"></div>
              <img class="img shadow-lg" v-if="animateToggle" :src="img" alt="">
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { TweenLite } from 'gsap'

export default {
  data: () => ({
    items: [
      {
        label: 'We are we want is',
        img: 'https://images.pexels.com/photos/2318776/pexels-photo-2318776.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940'
      },
      {
        label: 'We are we want is 2',
        img: 'https://images.pexels.com/photos/3393793/pexels-photo-3393793.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940'
      },
      {
        label: 'We are we want is 3',
        img: 'https://images.pexels.com/photos/3596282/pexels-photo-3596282.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940'
      },
    ],
    interval: null,
    currentIndex: 0,
    slideDuration: 5000,
    animateToggle: true,
  }),
  computed: {
    label() {
      return this.items[this.currentIndex].label
    },
    img() {
      return this.items[this.currentIndex].img
    }
  },
  mounted() {
    this.runSlideAnimation()
  },
  methods: {
    runSlideAnimation() {
      this.interval = setInterval(() => {
        this.nextSlide()
      }, this.slideDuration)
    },
    nextSlide() {
      if (this.currentIndex >= this.items.length -1) {
        this.currentIndex = 0
      } else {
        this.currentIndex++
      }
      this.animateToggle = false 
    },
    beforeEnter(el) {
      console.log('before enter', el)
      TweenLite.set(el, {
        y: '40%',
        autoAlpha: 0
      })
    },
    enter(el, done) {
      TweenLite.to(el, 1, {
        y: 0,
        autoAlpha: 1,
        onComplete() {
          done()
        }
      })
    },
    beforeLeave(el) {
      console.log('before leave.',el)
    },
    leave(el, done) {
      console.log('leave', el)
      let that = this
      TweenLite.to(el, .7, {
        y: '-40%',
        autoAlpha: 0,
        onComplete() {
          that.animateToggle = true
          done()
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../node_modules/mymixins/index';
.homepage-slider {
  @include size(100%, 100vh);
  @include flex-center();
  &--inner {
    position: relative;
    @include size(100%, auto);
    @include flex-center;
    .homepage-slider--label {
      width: 100%;
      text-align: center;
      font-size: 110px;
      color: #ff5f00;
      z-index: 5;
      @include breakpoint(phone) {
        font-size: 40px;
      }
    }
    .homepage-slider--img {
      @include size(100%, auto);
      @include absolute-center;
      @include flex-center;
      z-index: 4;
      .img-container {
        position: relative;
        @include size(300px, auto);
       
        .back-layer {
          @include size(100%, 100%);
          position: absolute;
          top: 0;
          left: 0;
          
        }
        img {
          width: 100%;
          height: auto;
          object-fit: cover;
          transform: rotate(-15deg);
          object-position: center;
        }
      }
    }
  }
}
</style>