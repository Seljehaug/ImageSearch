<template>
   <header id="header">
      <span class="logo-text-image">Image</span><span class="logo-text-search">Search</span>
   </header>
</template>

<script>
   export default {
      name: 'Header',
   };
</script>

<style scoped lang="scss">
   #header {
      height: 80px;
      letter-spacing: 0.025rem;
      position: absolute;
      display: flex;
      align-items: flex-start;
      flex-direction: column;
      justify-content: center;


      padding: 0.5rem;
      background: #39425c;
      z-index: 100;
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
</style>