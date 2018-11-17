<template>
   <div id="image-grid">
      {{ images }}
   </div>
</template>

<script>
   export default {
      name: 'ImageGrid',
      props: {
         images: Array
      },
      created() {
      }
   }
</script>

<style scoped>

</style>