<template>
    <div id="app">
        <MenuBar @emit-text="setSearchText" @emit-trending="trendingGifs"></MenuBar>
        <!-- <CarouselGifs v-bind:gifs="gifs"></CarouselGifs> -->
        <h1 style="margin: 30px;">{{ title }}</h1>
        <h2 style="margin: 30px;">Displaying {{ limit }} Gifs</h2>
        <div>
            <ul>
                <li class="gif-item" v-for="gif in gifs" v-bind:key="gif.id">
                    
                    <div v-bind:src="gif.images.fixed_height_small.url" v-bind:style="buildGifPlaceholder(gif)" v-if=true>
                        <a v-bind:src="gif.images.fixed_height_small.url"><img style="position: absolute; z-index: 10;" v-cloak v-bind:src="gif.images.fixed_height_small.url" alt=""></a>
                 
                    <svg style="z-index:-1" v-bind:width="gif.images.fixed_height_small.width" v-bind:height="gif.images.fixed_height_small.height">
                    </svg>
                        
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import MenuBar from './MenuBar';
import CarouselGifs from './CarouselGifs';
export default {
    name: 'GiphyAPI',
    props: {
        msg: String
    },
    components: {
    MenuBar,
    CarouselGifs,
  },
    data() {
        return{
        title: "Trending Gifs",
        apikey: "BnHDTmMLviwT2Jhowt3GNZsFATVXxR2V",
        searchText: "",
        limit: 25,
        gifs: [],
        imgLoaded: 0,
        loaded: false,
        result: ""}
    },
    mounted() {
        this.trendingGifs();
    },
    updated(){
        console.log("updated");
    },

    methods: {
        buildURL: function(){
            let texto = this.replaceSpaces(this.searchText);
            return "http://api.giphy.com/v1/gifs/search?q=" + texto + "&api_key=" + this.apikey + "&limit=" + this.limit;
        },
        buildGifPlaceholder: function(gif){
            this.result = "margin: 2px; width: " + 
            gif.images.fixed_height_small.width + "; height: " + gif.images.fixed_height_small.height + "; background-color: black;";
            return this.result;
        },
        searchGifs: function(){
            axios.get(this.buildURL())
            .then(response => {this.gifs = response.data.data});
            this.title = "Results for '" + this.searchText + "'";
        },
        trendingGifs: function(){
            axios.get("http://api.giphy.com/v1/gifs/trending?api_key=" + this.apikey)
            .then(response => {
            this.gifs = response.data.data;
            this.title = "Trending Gifs";
            this.setSearchText("", 25);
            });
        },

        replaceSpaces: function(string){
            return string.replace(" ", "+");
        },
        setSearchText: function(text, limit){
            if((text == undefined) || text.trim() == "" ){
                return;
            }
            this.limit = limit;
            this.searchText = text;
            this.searchGifs();
        },
        handleLoad: function(todo){
            todo.target.style.visibility = "visible";
            this.loaded=false;
    	    this.imgLoaded++;
            if(this.imgLoaded === this.gifs.length) {
              console.log('all image loaded')	
              this.loaded=true;
            }
        },

            
    }
}
</script>

<style>
    @import url(https://fonts.googleapis.com/css?family=Open+Sans);
    [v-cloak] { display:none; }
    [v-cloak]::before { content: "loading..."; }
    body{
    background: #f2f2f2;
    font-family: 'Open Sans', sans-serif;
    }

    .gif-item{
        display: inline-block
    }

    .search {
    width: 100%;
    position: relative;
    display: flex;
    }

    .searchTerm {
    width: 100%;
    border: 3px solid #00B4CC;
    border-right: none;
    padding: 5px;
    height: 20px;
    border-radius: 5px 0 0 5px;
    outline: none;
    color: #9DBFAF;
    }

    .searchTerm:focus{
    color: #00B4CC;
    }

    .searchButton {
    width: 40px;
    height: 36px;
    border: 1px solid #00B4CC;
    background: #00B4CC;
    text-align: center;
    color: #fff;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
    font-size: 20px;
    }

    /*Resize the wrap to see the search bar change!*/
    .wrap{
    width: 30%;

    top: 50%;
    left: 50%;
    transform: translate(100%, -50%);
    }

</style>