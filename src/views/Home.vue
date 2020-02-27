<template>
  <div class="home">
    <Header />
    <div class="section-1">
      <div class="container mx-auto">
        <div class="text-5xl text-center text-gray-900">
          We specialize in mobile apps. In fact, that’s the only thing we do, so we have well-established processes and a well-coordinated team of developers.
          Take a look
          mobile apps launched
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Header from '@/components/Header.vue'

export default {
  name: 'Home',
  components: {
    Header
  },
}
</script>

<style lang='scss'>
.home {
  min-height: 300vh;
}
  .header {
    width: 100%;
    height: 30vh;
    background-color: tomato;
  }
</style>
