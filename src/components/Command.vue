<template>
  <div class="command-container font-mono text-sm shadow-lg rounded-lg bg-gray-900 text-white m-2 fixed z-10 py-3 px-5">
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
</template>

<script>
export default {
  data: () => ({
    commandType: '',
    template: '',
    templateList: [

    ]
  }),
  watch: {
    commandType(type) {
      console.log('type' , type)
    },
    templateList(tpl) {
      console.log('tpl list', tpl)
    }
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
}
</style>