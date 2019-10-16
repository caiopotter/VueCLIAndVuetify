<template>
  <div class="home">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <GiphyAPI msg="Trending"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import GiphyAPI from '@/components/GiphyAPI.vue'

export default {
  name: 'home',
  components: {
    GiphyAPI
  }
}
</script>
