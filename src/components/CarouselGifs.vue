<template>
  <v-carousel v-model="carouselIndex"
  :height="gifHeight" 
  :hide-delimiters=true>
    <v-carousel-item 
      v-for="(gif, i) in gifs"
      :key="i"
      :src="gif.images.original_still.url" :style="mountCarouselStyle(gif)"
    >
      
    </v-carousel-item>
  </v-carousel>
</template>

<script>
  export default {
    data () {
      return {
        colors: [
          'primary',
          'secondary',
          'yellow darken-2',
          'red',
          'orange',
        ],
        gifHeight: 200,
        carouselIndex: 0,
      }
    },
    watch: {
        carouselIndex: function(){
            this.gifHeight = this.gifs[this.carouselIndex].images.original.height;
        }
    },
    methods:{
        mountCarouselStyle: function(gif){
            return "width: " + gif.images.original_still_width + "px;";
        }
    },
    props: {
        gifs: {

      }
    },
    }
</script>