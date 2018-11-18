<template>
   <div id="app">
      <div class="inner">
         <Header/>
         <SearchBar :searchText="searchText" v-on:getSearchText="fetchImages($event)"/>
         <ImageGrid :images="images"/>
         <ImageDetails/>
      </div>
   </div>
</template>

<script>
   // Unsplash API
   import API_CONFIG from '../API_CONFIG.js';
   import Unsplash from 'unsplash-js';
   
   // Components
   import Header from './components/Header.vue';
   import SearchBar from './components/SearchBar.vue';
   import ImageGrid from './components/ImageGrid.vue';
   import ImageDetails from './components/ImageDetails.vue';

   export default {
      name: 'app',
      components: {
         Header,
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

         this.unsplash.photos.listPhotos(1, 50, "latest").then(res => {
            res.json().then(images => {
               this.images = images;
               console.log(this.images);
            });
         });
      },

      methods: {
         fetchImages: function(text){
            this.searchText = text;

            this.unsplash.search.photos(this.searchText, 1, 50).then(res => {
               res.json().then(data => {
                  this.images = data.results;
               });
            });
         }
      }
   };
</script>

<style lang="scss">
   @import '~normalize-scss/sass/normalize/_import-now.scss';

   * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
   }

   #app {
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
   }

   .inner {
      max-width: 1600px;
      margin: 0 auto;
      // width: calc(100% - 1rem);
      width: 100%;
      // padding: 0.5rem;s
   }
</style>
