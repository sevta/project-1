<template>
  <div class="homepage-slider-container">
    <div class="homepage-slider font-sans">
      <div class="homepage-slider--inner">
        <transition name='fadeUp'>
          <div class="homepage-slider--label text-left text-gray-900 font-heading text-tBlack text-shadow" v-if="animateToggle" v-html="label"></div>
        </transition>
        <div class="homepage-slider--img">
          <transition
            v-on:before-enter="beforeEnter"
            v-on:enter="enter"
            v-on:before-leave="beforeLeave"
            v-on:leave="leave"
          >
            <div class="img-container shadow bg-gray-200" v-if="animateToggle">
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
        label: 'Lorem ipsum dolor, sit amet consectetur <span class="text-tRed">adipisicing</span> elit. A quas sequi vitae harum similique molestias neque iure! Dolorum totam accusantium neque corrupti quidem iusto cum, laborum provident facilis. Quos, itaque.',
        img: 'https://images.pexels.com/photos/2318776/pexels-photo-2318776.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940'
      },
      {
        label: 'Lorem ipsum dolor, sit amet consectetur <span class="text-tRed">adipisicing</span> elit. A quas sequi vitae harum similique molestias neque iure! Dolorum totam accusantium neque corrupti quidem iusto cum, laborum provident facilis. Quos, itaque.',       
        img: 'https://images.pexels.com/photos/3393793/pexels-photo-3393793.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940'
      },
      {
        label: 'Lorem ipsum dolor, sit amet consectetur <span class="text-tRed">adipisicing</span> elit. A quas sequi vitae harum similique molestias neque iure! Dolorum totam accusantium neque corrupti quidem iusto cum, laborum provident facilis. Quos, itaque.',
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
    justify-content: flex-start;
    .homepage-slider--label {
      position: relative;
      width: 50%;
      text-align: left;
      padding-left: 3vw;
      font-size: 45px;
      // color: #ff5f00;
      z-index: 5;
      &::before {
        display: none;
        content: '';
        @include size(50%, 4px);
        background-color: black;
        position: absolute;
        bottom: -5px;
        right: 0px;
      }
      @include breakpoint(phone) {
        font-size: 40px;
      }
    }
    .homepage-slider--img {
      @include size(100%, auto);
      @include absolute-center;
      @include flex-center;
      justify-content: flex-end;
      padding-right: 10vw;
      z-index: 4;
      .img-container {
        position: relative;
        @include size(350px, auto);
       
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