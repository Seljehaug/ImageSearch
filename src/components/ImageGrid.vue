<template>
   <div id="image-grid">
      
      <div class="image-wrapper" v-for="(image, index) in images" :key="image.id">
         <div class="image" :data-image-position="index" 
            :style="{'background-image': `url(${image.urls.small})`}"
            v-on:click="openLightBox($event)">
         </div>
      </div>

      <LightBox :images="images" :activeImagePos="activeImagePos" :activeImage="activeImage" :lightBoxIsActive="lightBoxIsActive" 
         v-on:closeLightBox="closeLightBox($event)"
         v-on:prevImage="prevImage"
         v-on:nextImage="nextImage"/>

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
            lightBoxIsActive: false,
            activeImage: null
         }
      },
      
      methods: {
         openLightBox: function(event) {
            const imagePos = parseInt(event.target.dataset.imagePosition); 
            
            this.activeImagePos = imagePos; 
            this.activeImage = this.images[imagePos];
   
            if(this.activeImage !== null){
               this.lightBoxIsActive = true;
            }
         },

         closeLightBox: function(status){
            console.log(status)
            this.lightBoxIsActive = status;
         },

         prevImage: function(){
            // TODO: exception for when clicking previous on the first image

            this.activeImagePos = this.activeImagePos - 1;
            this.activeImage = this.images[this.activeImagePos];
         },

         nextImage: function(){
            // TODO: exception for when clicking next on the last image

            this.activeImagePos = this.activeImagePos + 1;
            this.activeImage = this.images[this.activeImagePos];
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