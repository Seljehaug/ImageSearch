<template>
   <div id="search-bar">
      <div id="logo">
         <span class="logo-text-image">Image</span><span class="logo-text-search">Search</span>
      </div>
      <div class="search-bar-wrapper">
         <form v-on:submit.prevent="updateSearchText">
            <input class="search-field" type="text" placeholder="Search...">
            <label>
               <input class="search-btn" type="submit">
               <svg class="search-icon" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
                  width="612.08px" height="612.08px" viewBox="0 0 612.08 612.08" style="enable-background:new 0 0 612.08 612.08;"
                  xml:space="preserve">
                  <g>
                     <path d="M237.927,0C106.555,0,0.035,106.52,0.035,237.893c0,131.373,106.52,237.893,237.893,237.893
                     c50.518,0,97.368-15.757,135.879-42.597l0.028-0.028l176.432,176.433c3.274,3.274,8.48,3.358,11.839,0l47.551-47.551
                     c3.274-3.274,3.106-8.703-0.028-11.838L433.223,373.8c26.84-38.539,42.597-85.39,42.597-135.907C475.82,106.52,369.3,0,237.927,0z
                     M237.927,419.811c-100.475,0-181.918-81.443-181.918-181.918S137.453,55.975,237.927,55.975s181.918,81.443,181.918,181.918
                     S338.402,419.811,237.927,419.811z" />
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g>
                  <g>
                  </g></svg>
            </label>
         </form>
      </div>
   </div>
</template>

<script>
   import Headroom from 'headroom.js/dist/headroom.js';

   export default {
      name: 'SearchBar',
      props: {
         searchText: String
      },

      data() {
         return {
            searchBarElement: null
         };
      },

      mounted() {
         // Set up Headroom for showing/hiding search-bar on scroll
         this.searchBarElement = document.getElementById('search-bar');
         const headroom = new Headroom(this.searchBarElement, {
            offset: this.searchBarElement.offsetHeight,
            classes: {
               initial: 'headroom',
               pinned: 'scroll-up',
               unpinned: 'scroll-down',
               top: 'above-offset',
               notTop: 'not-top',
               bottom: 'bottom',
               notBottom: 'not-bottom'
            }
         });
         headroom.init();
      },

      methods: {
         updateSearchText: function(){
            const searchField = document.querySelector('#search-bar input');

            this.$emit('getSearchText', searchField.value);
         }
      }
   };
</script>

<style scoped lang="scss">
   #search-bar {
      height: 80px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 0 0.5rem 0;
      background-color: #4D5D8B;
      position: fixed;
      left: 0;
      right: 0;
      top: 0;
      transition: top ease-in-out 300ms;
      border-bottom: 2px solid transparent; 
      z-index: 50;

      &.scroll-up { // scrolling up
         top: 0;
         transition: top ease-in-out 300ms;
         border-color: white;

         #logo {
            top: -2px; // same as border in #search-bar
            transition: top ease-in-out 100ms;
         }
      }

      &.scroll-down { // scrolling down
         top: -80px;
         transition: top ease-in-out 300ms;
         border-color: transparent;

         #logo {
            top: 0;
            transition: top ease-in-out 100ms;
         }
      }

      #logo {
         height: 80px;
         letter-spacing: 0.025rem;
         position: absolute;
         left: 0;
         display: flex;
         align-items: flex-start;
         flex-direction: column;
         justify-content: center;
         padding: 0.5rem;
         background: #39425c;
         z-index: 50;
         top: 0;

         .logo-text-image {
            font-size: 1rem;
            font-weight: bold;
            color: #4fd3e8;
         }

         .logo-text-search {
            margin-left: 0.75rem;
            font-weight: bold;
            color: #4fd3e8;
            font-size: 1.25rem;
            border-bottom: 1px solid;
         }
      }

      .search-bar-wrapper {
         max-width: 300px;
         width: 100%;
         display: flex;
         align-items: center;
         margin-top: 2px; // same as border-bottom on #search-bar
      }

      form {
         width: 100%;
         display: flex;
         height: 40px;
         position: relative;
      }

      .search-field {
         width: 100%;
         padding: 0.5rem;
         height: 40px;
         background: #39425c;
         color: #e8eeff;
         border: 1px solid #39425c;
         border-top-left-radius: 3px;
         border-bottom-left-radius: 3px;

         &:focus {
            outline: none; 
            border: 1px solid #a8b6db;
         }
      }

      ::-webkit-input-placeholder { /* Chrome/Opera/Safari */
         color:#e8eeff;
      }
      ::-moz-placeholder { /* Firefox 19+ */
         color:#e8eeff;
      }
      :-ms-input-placeholder { /* IE 10+ */
         color:#e8eeff;
      }
      :-moz-placeholder { /* Firefox 18- */
         color:#e8eeff;
      }

      .search-btn {
         width: 40px;
         height: 40px;
         background: #a8b6db;
         color: #a8b6db;
         border: none;
         border-top-right-radius: 3px;
         border-bottom-right-radius: 3px;
         font-size: 0;

         &:focus, &:hover {
            background: #39425c;
            color: #39425c;
            outline: none;
            border: 1px solid #a8b6db;
         }

         &:focus + .search-icon, &:hover + .search-icon {
            fill: #a8b6db;
         }
      }

      .search-icon {
         width: 1.25rem;
         height: 1.25rem;
         position: absolute;
         right: 10px;
         top: 10px;
         pointer-events: none;
         fill: #39425c;
      }
   }

   @media(max-width: 600px) {
      #search-bar #logo {
         display: none;
      }
   }
</style>