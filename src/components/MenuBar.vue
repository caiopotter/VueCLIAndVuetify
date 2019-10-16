<template>
  <div>
    <v-toolbar>
      <v-toolbar-title>Teste Vue/Vuetify</v-toolbar-title>

    <v-text-field style="margin-left: 30px;" v-model="searchText"
        hide-details
        placeholder="Your search goes here!"
        single-line
    ></v-text-field>
    <v-btn @click="$emit('emit-text', searchText, gifsLimit)" icon>
        <v-icon>mdi-magnify-outline</v-icon>
    </v-btn>
      <v-spacer></v-spacer>
        

      <v-toolbar-items>
        <v-btn text @click="$emit('emit-trending')">Trending</v-btn>
      </v-toolbar-items>

      <template v-if="$vuetify.breakpoint.smAndUp">
        <v-btn @click="$emit('emit-text', searchText, 10)" icon>
          10
        </v-btn>
        <v-btn @click="$emit('emit-text', searchText, 25)" icon>
          25
        </v-btn>
        <v-btn @click="$emit('emit-text', searchText, 50)" icon>
          50
        </v-btn>
      </template>
    </v-toolbar>
  </div>
</template>

<script>
export default {
    name: 'MenuBar',
    props: {
        msg: String
    },
    data() {
        return{
        searchText: "",
        gifsLimit: 25
       }
    },
    methods: {
        setGifsLimit: function(limit){
            this.gifsLimit = limit;
        }
    }
}

</script>

<style scoped>
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