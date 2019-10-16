<template>
  <v-app>

    <v-content>
      <GiphyAPI/>
    </v-content>
  </v-app>
</template>

<script>
import GiphyAPI from './components/GiphyAPI';

export default {
  name: 'App',
  components: {
    GiphyAPI,
  },
  data: () => ({
    //
  }),
};
</script>
