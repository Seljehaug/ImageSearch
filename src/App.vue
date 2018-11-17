<template>
   <div id="app">
      <SearchBar :searchText="searchText" v-on:getSearchText="fetchImages($event)"/>
      <ImageGrid :images="images"/>
      <ImageDetails msg="Image here.."/>
   </div>
</template>

<script>
   // Unsplash API
   import API_CONFIG from '../API_CONFIG.js';
   import Unsplash from 'unsplash-js';
   
   // Components 
   import SearchBar from './components/SearchBar.vue';
   import ImageGrid from './components/ImageGrid.vue';
   import ImageDetails from './components/ImageDetails.vue';

   export default {
      name: 'app',
      components: {
         SearchBar,
         ImageGrid,
         ImageDetails
      },
      
      data: function() {
         return {
            API_KEY: null,
            API_SECRET: null,
            images: [],
            searchText: null,
            unsplash: null
         };
      },
      
      created() {
         this.API_KEY = API_CONFIG.API_KEY;
         this.API_SECRET = API_CONFIG.API_SECRET;

         this.unsplash = new Unsplash({
            applicationId: this.API_KEY,
            secret: this.API_SECRET,
            callbackUrl: ""
         });

         this.unsplash.photos.listPhotos(1, 20, "latest").then(res => {
            res.json().then(data => {
               console.log(data);
            });
         });
      },

      methods: {
         fetchImages: function(text){
            this.searchText = text;
         }
      }
   };
</script>

<style>
   #app {
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
      margin-top: 60px;
   }
</style>
