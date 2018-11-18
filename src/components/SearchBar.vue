<template>
   <div id="search-bar">
      <form v-on:submit.prevent="updateSearchText">
         <input type="text" placeholder="Search for something...">
         <!-- <input type="submit">

         </input> -->
      </form>

      
   </div>
</template>

<script>
   export default {
      name: 'SearchBar',
      props: {
         searchText: String
      },

      // data(){
      //    return {
      //       inputText: null
      //    }
      // },

      created() { 
      
      },
      
      methods: {
         updateSearchText: function(){
            const searchField = document.querySelector('#search-bar input');

            this.$emit('getSearchText', searchField.value);
         }
      }
   }
</script>

<style scoped>

</style>