<template>
   <div id="search-bar">
      {{ searchText }}
   </div>
</template>

<script>
   export default {
      name: 'SearchBar',
      props: {
         searchText: String
      },
      created() {
         const text = "Updated";

         this.$emit('getSearchText', text);
      }
   }
</script>

<style scoped>

</style>