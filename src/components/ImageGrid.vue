<template>
   <div id="image-grid">
      
      <div class="image-wrapper" v-for="(image, index) in images" :key="image.id">
         <div class="image" :data-image-position="index" 
            :style="{'background-image': `url(${image.urls.small})`}"
            v-on:click="openLightBox($event)">
         </div>
      </div>

      <LightBox :images="images" :activeImagePos="activeImagePos" :lightBoxIsActive="lightBoxIsActive" v-on:closeLightBox="closeLightBox($event)"/>

   </div>
</template>

<script>
   import LightBox from './LightBox.vue';

   export default {
      name: 'ImageGrid',
      
      components: {
         LightBox
      },
      
      props: {
         images: Array
      },
      
      data() {
         return {
            activeImagePos: null,
            lightBoxIsActive: false
         }
      },
      
      methods: {
         openLightBox: function(event) {
            const imagePos = parseInt(event.target.dataset.imagePosition); 
            this.activeImagePos = imagePos; 

            if(this.activeImagePos !== null){
               this.lightBoxIsActive = true;
            }
         },

         closeLightBox: function(status){
            console.log(status)
            this.lightBoxIsActive = status;
         }
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