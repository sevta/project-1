<template>
  <transition 
    v-on:before-enter="beforeEnter"
    v-on:enter="enter"
    v-on:after-enter="afterEnter"
    v-on:enter-cancelled="enterCancelled"

    v-on:before-leave="beforeLeave"
    v-on:leave="leave"
  >
    <div v-if="show" class='menu z-30 p-3 fixed top-0 left-0 w-full h-screen bg-teal-200'>
      <div class="layer layer-1 bg-teal-300"></div>
      <div class="layer layer-2 bg-teal-400"></div>
      <div class="layer layer-3 bg-teal-500 p-3 text-white flex items-center justify-center font-sans">
        <div class="close font-bold absolute top-0 right-0 cursor-pointer" @click="onCloseClick">close</div>
        <div class="list-menu-container flex flex-col text-3xl font-bold uppercase">
          <div class="list-menu">Home</div>
          <div class="list-menu">Aduh</div>
          <div class="list-menu">Aduh</div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import { TweenLite, TimelineMax } from 'gsap'
export default {
  props: {
    show: {
      type: Boolean
    }
  },
  methods: {
    onCloseClick() {
      this.$store.commit('toggleMenu', false)
    },
    beforeEnter(el) {
      TweenLite.set(el, {
        y: '-100vh'
      })
      el.children.forEach(el => {
        TweenLite.set(el, {
          y: '-100%'
        })
      })
      let listMenu = el.children[2].children
      console.log(listMenu)
    },
    animateLayer(el) {
      TweenLite.to(el, .8, {
        y: 0
      })
    },
    enter(el, done) {
      console.log('enter')
      let that = this
      let tick = 0
      let layer = document.querySelectorAll('.layer')
      let listMenu = document.querySelectorAll('.list-menu')

      TweenLite.to(el, .6, {
        y: 0,
        onUpdate() {
          tick++
          if (tick == 12) {
            that.animateLayer(layer[0])
          }
          if (tick == 18) {
            that.animateLayer(layer[1])
          }
          if (tick == 32) {
            that.animateLayer(layer[2])
          }
        },
        onComplete() {
          let tl = new TimelineMax({
            onComplete() {
              done()
            }
          })
          tl.staggerTo(listMenu, .6, {
            autoAlpha: 1,
            y: 0,
          }, .2)
        }
      })
    },
    afterEnter(el) {
      console.log('after enter')
    },
    enterCancelled(el) {
      console.log('enter cancelled')
    },
    beforeLeave(el) {      
      let layers = document.querySelectorAll('.layer')
      console.log('before leave...', layers)
    },
    leave(el, done) {
      let layers = document.querySelectorAll('.layer')
      let tl = new TimelineMax({
        onComplete() {
          done()
        }
      })

      tl
        .to(layers[2], .5, {
          autoAlpha: 0
        })
        .to(layers[1], .6, {
          width: window.innerWidth / 2,
          height: window.innerWidth / 2,
          scale: .3,
          borderRadius: '50%'
        }, .7)
        .to(layers[1], .4, {
          y: '-100%',
          x: '100%',
          autoAlpha: 0
        })
        .to(el, .4, {
          y: '100%'
        })      
    }
  }
}
</script>

<style lang="scss" scoped>
.menu {
  .layer-1, .layer-2, .layer-3 {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    .list-menu-container {
      .list-menu {
        opacity: 0;
        transform: translateY(120px);
      }
    }
  }
}
</style>