<template>
  <div class="home">
    <Header />
    <div class="section-1">
      <div class="container mx-auto px-5 md:px-0">
        <div class="text-4xl md:text-3xl text-center">
          <!-- We specialize in mobile apps. In fact, that’s the only thing we do, so we have well-established processes and a well-coordinated team of developers.
          Take a look
          mobile apps launched -->
        </div>
        <div class="btn-container flex items-center justify-center">
          <Button />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header'
import Button from '@/components/Button'

export default {
  name: 'Home',
  components: {
    Header,
    Button
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
