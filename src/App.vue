<template>
   <div id="app">
      {{ API_KEY }}
      {{ API_SECRET }}
   </div>
</template>

<script>
   import API_CONFIG from '../API_CONFIG.js';

   export default {
      name: 'app',
      components: {

      },
      data: function() {
         return {
            API_KEY: null,
            API_SECRET: null
         };
      },
      created() {
         this.API_KEY = API_CONFIG.API_KEY;
         this.API_SECRET = API_CONFIG.API_SECRET;
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
