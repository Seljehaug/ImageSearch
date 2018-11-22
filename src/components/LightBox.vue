<template>
   <div id="light-box" :class="lightBoxClass">
      
      <div class="overlay"></div>

      <button v-on:click="prevImage" class="previous">Previous</button>
      <img :src="backgroundImage" alt="">
      <button v-on:click="nextImage" class="next">Next</button>

      <button v-on:click="closeLightBox" class="close">Close</button>

   </div>
</template>

<script>
   export default {
      name: 'LightBox',
      props: {
         images: Array,
         activeImagePos: Number,
         lightBoxIsActive: Boolean,
         activeImage: Object
      },

      created() {
         document.addEventListener('keyup', this.handleKeyUp);
      },

      computed: {
         backgroundImage: function() {
            return (this.lightBoxIsActive && this.activeImage !== null) 
               ? this.activeImage.urls.regular 
               : "";
         },
         lightBoxClass: function(){
            return this.lightBoxIsActive ? "lightbox-active" : "lightbox-inactive";
         }
      },

      methods: {
         closeLightBox: function(){
            this.$emit('closeLightBox', false);
         },
         prevImage: function(){
            this.$emit('prevImage');
         },
         nextImage: function(){
            this.$emit('nextImage');
         },
         handleKeyUp: function(event) {
            if(!this.lightBoxIsActive) return; 
            
            if (event.key !== undefined) {
               const key = event.key; 

               switch(key){
                  case 'ArrowLeft':
                     this.prevImage();
                     break;
                  case 'ArrowRight':
                     this.nextImage();
                     break;
                  case 'Escape':
                     this.closeLightBox();
                     break;
                  default: 
                     break;
               } 
            }

            else if (event.keyCode !== undefined) {
               const keyCode = event.keyCode;

               switch(keyCode){
                  case 37:
                     this.prevImage();
                     break;
                  case 39:
                     this.nextImage();
                     break;
                  case 27:
                     this.closeLightBox();
                     break;
                  default: 
                     break;
               } 
            }
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
      z-index: 100;
      background-size: cover;

      &.lightbox-active {
         display: flex;
         justify-content: center;
         align-items: center;
      }

      &.lightbox-inactive {
         display: none;
      }

      img {
         min-width: 400px;
         max-width: 100%;
         max-height: 100%;
         z-index: 100;
         background: black;
         padding: 1rem;
      }
   }

   .light-box-content {
      z-index: 100;
      max-width: 100%;
      max-height: 100%;
   }

   .overlay {
      position: fixed;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      background: black;
      opacity: 0.8;
   }

   .previous, .next {
      z-index: 100;
      height: 100%;
      width: 100px;
      background-color: black;
      color: white;
      border: none;
   }

   .close {
      position: absolute;
      top: 0;
      right: 0;
      z-index: 100;
   }
</style>