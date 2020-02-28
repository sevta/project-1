<template>
  <div  class="command-container font-mono text-sm shadow-lg rounded-lg bg-tBlack overflow-hidden text-white m-2 py-12 fixed z-10 py-3 px-5">
    <div class="nav-pane-top cursor-drop w-full py-2 px-3 bg-tWhite absolute top-0 left-0">
      <div class="text-black flex items-center">
        <div class="pane-btn cursor-pointer bg-red-600 mr-2"></div>
        <div class="pane-btn cursor-pointer bg-yellow-600 mr-2" @click="minimize"></div>
        <div class="pane-btn cursor-pointer bg-green-600"  @click="maximize"></div>
      </div>
    </div>
    <div class="command-inner" v-if="showCmmandInner">
      <div class="flex" v-for="(tpl, index) in templateList" :key="index">
        <div v-html="tpl"></div>
      </div>
      <div class="flex">
        <div><span class="text-yellow-600 font-bold">@Sevta</span>:~$ </div>
        <div>
          <input type="text" placeholder="type.." class="bg-transparent px-3" v-model="commandType" @keydown.enter="onEnterType">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { TweenLite } from 'gsap'

export default {
  data: () => ({
    commandType: '',
    template: '',
    templateList: [

    ],
    showCmmandInner: false
  }),
  watch: {
    commandType(type) {
      console.log('type' , type)
    },
    templateList(tpl) {
      console.log('tpl list', tpl)
    }
  },
  mounted() {
    this.minimize()
  },
  methods: {
    command(type) {
      if (type == 'help') {
        this.template = `
          <div>
            <div>help :(</div>
          </div>
        `
      } 
      if (type == 'cls') {
        this.templateList = []
      }
    },
    onEnterType() {
      this.command(this.commandType)
      this.templateList.push(this.template)
      this.commandType = ''
    },
    minimize() {
      this.showCmmandInner = false
      this.runMinimizeAnimation()
    },
    maximize() {
      this.showCmmandInner = true 
      this.runMaximizeAnimation()
    },
    runMaximizeAnimation() {
      let $command = document.querySelector('.command-container')
      let $commandInner = document.querySelector('.command-inner')
      
      TweenLite.to($command, .3, {
        width: 600,
        y: 0,
        height: 600
      })

      $command.classList.add('py-12')
    },
    runMinimizeAnimation() {
      let $command = document.querySelector('.command-container')
      let $commandInner = document.querySelector('.command-inner')
      $command.classList.remove('py-12')
      TweenLite.to($command, .2, {
        y: window.innerHeight - 60,
        width: 70,
        height: '30px',
        padding: '10px'
      })
    },
    enter() {

    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../node_modules/mymixins/index';

.command-container {
  @include size(600px, 600px);
  input {
    outline: unset;
  }
  .pane-btn {
    @include size(12px, 12px);
    border-radius: 50%;
  }
}
</style>