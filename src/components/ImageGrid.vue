<template>
   <div id="image-grid">
      
      <div class="image-wrapper" v-for="image in images" :key="image.id">
         <div class="image" :style="{'background-image': `url(${image.urls.small})`}"></div>
      </div>

   </div>
</template>

<script>
   export default {
      name: 'ImageGrid',
      props: {
         images: Array
      }
   };
</script>

<style scoped lang="scss">
   #image-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      grid-gap: 0.5rem;
      padding: 0 0.5rem 0.5rem 0.5rem;

      .image-wrapper {
         border: 1px solid white;
         height: 200px;
         position: relative;

         .image {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-size: cover;
         }
      }
   }
</style>