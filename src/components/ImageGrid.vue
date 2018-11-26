<template>
   <div id="image-grid">
      
      <div class="image-wrapper" tabindex="0" v-for="(image, index) in images" :key="image.id">
         <div class="image" :data-image-position="index" 
            :style="{'background-image': `url(${image.urls.small})`}"
            v-on:click="openLightBox($event)">
         </div>
         <div class="image-overlay"></div>
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
         };
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
            this.lightBoxIsActive = status;
         },

         prevImage: function(){
            this.activeImagePos = this.activeImagePos === 0 
               ? this.images.length -1 
               : this.activeImagePos -1;

            this.activeImage = this.images[this.activeImagePos];
         },

         nextImage: function(){
            this.activeImagePos = this.activeImagePos === this.images.length - 1
               ? 0 
               : this.activeImagePos + 1;

            this.activeImage = this.images[this.activeImagePos];
         }
      }
   };
</script>

<style scoped lang="scss">
   #image-grid {
      // Flexbox fallback for browsers not supporting grid 
      display: flex;
      flex-wrap: wrap;
      justify-content: center;

      .image-wrapper {
         border: 1px solid white;
         height: 200px;
         min-width: 200px;
         position: relative;
         cursor: pointer;

         &:hover, &:focus {
            outline: none;

            .image-overlay {
               // display: block;
               opacity: 0.25;
               transition: opacity 150ms ease-in-out;
            }
         }

         .image {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #333333;
            background-size: cover;
            background-position: center;
         }

         .image-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: black;
            opacity: 0;
            pointer-events: none;
            transition: opacity 150ms ease-in-out;
         }
      }
   }
   
   @supports(display: grid){
      #image-grid {
         display: grid;
         grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
         grid-gap: 0.5rem;
         padding: 0 0.5rem 0.5rem 0.5rem;
      }
   }
  
</style>