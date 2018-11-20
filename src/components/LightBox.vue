<template>
   <div id="light-box" :class="lightBoxClass" 
   >
   <!-- :style="{'background-image': `url(${backgroundImage})`}" -->
      
         <img :src="backgroundImage" alt="">
         
         <button v-on:click="closeLightBox" class="close">Close</button>

         <div class="overlay"></div>

   </div>
</template>

<script>
   export default {
      name: 'LightBox',
      props: {
         images: Array,
         activeImagePos: Number,
         lightBoxIsActive: Boolean
      },

      methods: {
         closeLightBox: function(){
            this.$emit('closeLightBox', false);
         }
      },

      computed: {
         backgroundImage: function() {
            return (this.lightBoxIsActive && this.activeImagePos !== null) 
               ? this.images[this.activeImagePos].urls.regular 
               : "";
         },
         lightBoxClass: function(){
            return this.lightBoxIsActive ? "lightbox-active" : "lightbox-inactive";
         }
      }
   };
</script>

<style scoped lang="scss">
   #light-box {
      position: fixed;
      top: 2rem;
      left: 2rem;
      right: 2rem;
      bottom: 2rem;
      background: transparent;
      border: 1px solid black;
      z-index: 100;
      background-size: cover;
      max-width: 800px;
      margin: 0 auto;

      &.lightbox-active {
         display: flex;
         justify-content: center;
         align-items: center;
      }

      &.lightbox-inactive {
         display: none;
      }

      img {
         max-width: 100%;
         max-height: 100%;
      }
   }

   // .overlay {
   //    position: fixed;
   //    top: 0;
   //    right: 0;
   //    bottom: 0;
   //    left: 0;
   //    background: black;
   // }
</style>