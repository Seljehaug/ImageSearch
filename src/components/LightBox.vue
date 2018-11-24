<template>
   <div id="light-box" :class="lightBoxClass">
      
      <div class="overlay"></div>

      <button v-on:click="prevImage" class="previous-btn">
         <svg class="arrow arrow-left" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
            width="451.847px" height="451.847px" viewBox="0 0 451.847 451.847" style="enable-background:new 0 0 451.847 451.847;"
            xml:space="preserve">
            <g>
               <path d="M97.141,225.92c0-8.095,3.091-16.192,9.259-22.366L300.689,9.27c12.359-12.359,32.397-12.359,44.751,0
               c12.354,12.354,12.354,32.388,0,44.748L173.525,225.92l171.903,171.909c12.354,12.354,12.354,32.391,0,44.744
               c-12.354,12.365-32.386,12.365-44.745,0l-194.29-194.281C100.226,242.115,97.141,234.018,97.141,225.92z" />
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
         </svg>
      </button>

      <img :src="backgroundImage" alt="">
      
      <button v-on:click="nextImage" class="next-btn">
         <svg class="arrow arrow-right" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
            width="451.847px" height="451.847px" viewBox="0 0 451.847 451.847" style="enable-background:new 0 0 451.847 451.847;"
            xml:space="preserve">
            <g>
               <path d="M97.141,225.92c0-8.095,3.091-16.192,9.259-22.366L300.689,9.27c12.359-12.359,32.397-12.359,44.751,0
               c12.354,12.354,12.354,32.388,0,44.748L173.525,225.92l171.903,171.909c12.354,12.354,12.354,32.391,0,44.744
               c-12.354,12.365-32.386,12.365-44.745,0l-194.29-194.281C100.226,242.115,97.141,234.018,97.141,225.92z" />
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
         </svg>
      </button>

      <button v-on:click="closeLightBox" class="close-btn">
         <svg class="close-icon" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
            viewBox="0 0 212.982 212.982" style="enable-background:new 0 0 212.982 212.982;" xml:space="preserve">
            <g id="Close">
               <path style="fill-rule:evenodd;clip-rule:evenodd;" d="M131.804,106.491l75.936-75.936c6.99-6.99,6.99-18.323,0-25.312
               c-6.99-6.99-18.322-6.99-25.312,0l-75.937,75.937L30.554,5.242c-6.99-6.99-18.322-6.99-25.312,0c-6.989,6.99-6.989,18.323,0,25.312
               l75.937,75.936L5.242,182.427c-6.989,6.99-6.989,18.323,0,25.312c6.99,6.99,18.322,6.99,25.312,0l75.937-75.937l75.937,75.937
               c6.989,6.99,18.322,6.99,25.312,0c6.99-6.99,6.99-18.322,0-25.312L131.804,106.491z" />
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
            <g>
            </g>
         </svg>
      </button>

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
         window.addEventListener('keyup', this.handleKeyUp);
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
      opacity: 0.85;
   }

   .previous-btn, .next-btn {
      z-index: 100;
      height: 100%;
      width: 100px;
      background-color: black;
      color: white;
      border: none;
   }

   .arrow {
      fill: white;
      height: 50%;
      width: 50%;
   }

   .arrow-right {
      transform: rotate(180deg);
   }

   .close-btn {
      position: absolute;
      top: 0;
      right: 0;
      z-index: 100;
      width: 40px;
      height: 40px;
      background: black;
      border-radius: 100%;
      border: 1px solid white;
      padding: 0.5rem;

      svg {
         fill: white;
      }
   }
</style>