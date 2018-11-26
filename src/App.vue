<template>
   <div id="app">
      <div class="inner">
         <Header/>
         <SearchBar :searchText="searchText" v-on:getSearchText="showSearchResults($event)"/>
         <ImageGrid :images="images"/>
      </div>
   </div>
</template>

<script>
   // Unsplash API
   import API_CONFIG from '../API_CONFIG.js';
   import Unsplash from 'unsplash-js';

   // Polyfills 
   import 'promise-polyfill/src/polyfill';
   import 'whatwg-fetch';

   // Components
   import Header from './components/Header.vue';
   import SearchBar from './components/SearchBar.vue';
   import ImageGrid from './components/ImageGrid.vue';

   export default {
      name: 'app',
      components: {
         Header,
         SearchBar,
         ImageGrid
      },

      data: function() {
         return {
            API_KEY: null,
            API_SECRET: null,
            unsplash: null,
            images: [],
            pages: 1, // used to keep track of pages of images retrieved from Unsplash (chunks of 30)
            defaultCategory: 'latest', // possible categories: latest, oldest, popular 
            searchText: null,
            activeLightBoxImage: null,
            scrolled: false,
            isScrollBottom: false
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

         this.fetchImages();
         this.pages = this.pages + 1;

         window.addEventListener('scroll', this.handleScroll);
      },

      methods: {
         handleScroll: function() {
            const d = document.documentElement;
            this.scrolled = d.scrollTop > 0;

            const offset = parseInt(Math.ceil(d.scrollTop + window.innerHeight));
            const height = parseInt(d.offsetHeight);

            if (offset >= height - 200 && !this.isScrollBottom) {
               this.isScrollBottom = true;

               // Used to avoid the fetch to be fired multiple times, causing it to populate the grid with the same images 
               window.setTimeout(() => { 
                  this.isScrollBottom = false;
               }, 300);

               if(this.searchText === null){ // No search made, fetch more images using defaultCategory 
                  this.fetchImages();
               }else {
                  this.fetchImagesBySearch();
               }
            }

         },

         fetchImages: function() {
            this.unsplash.photos.listPhotos(this.pages + 1, 30, this.defaultCategory).then(res => {     
               res.json().then(images => {
                  images.forEach(img => {
                     this.images.push(img);
                  });
               });

               this.pages = this.pages + 1;               
            });
         },

         showSearchResults: function(text){
            this.searchText = text;
            this.images = [];
            this.pages = 0;
            this.fetchImagesBySearch();
         },

         fetchImagesBySearch: function() {
            this.unsplash.search.photos(this.searchText, this.pages + 1, 30).then(res => {
               res.json().then(data => {
                  data.results.forEach(img => {
                     this.images.push(img);
                  });
               });

               this.pages = this.pages + 1;
            });
         },
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
      width: 100%;
   }
</style>
