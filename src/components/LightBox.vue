<template>
   <div id="light-box" :class="lightBoxClass">
      
      <div class="overlay" v-touch:swipe="handleSwipe"></div>

      <div class="lightbox-content" v-touch:swipe="handleSwipe">

         <div class="controls-left">
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
         </div>

         <img :src="backgroundImage" alt="">
         
         <div class="controls-right">
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
         </div>

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
         
         handleSwipe: function(direction) {
            if(direction === 'left'){
               this.nextImage();
            }
            if(direction === 'right'){
               this.prevImage();
            }
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
      },
      
   };
</script>

<style scoped lang="scss">
   .lightbox-content {
      z-index: 50;
      position: relative;
      padding: 2rem 0;
      background: black;
   }

   #light-box {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: transparent;
      z-index: 100;
      background-size: cover;
      padding: 3rem calc(3rem + 5vw);

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
         z-index: 100;
         background: black;
         max-height: 80vh;
      }
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

   .controls-left, .controls-right {
      position: absolute;
      top: 0;
      bottom: 0;
      width: 5vw;
      display: flex;
   }

   .controls-left {
      left: -5vw;
   }

   .controls-right {
      right: -5vw;
   }

   .previous-btn, .next-btn {
      z-index: 100;
      height: 100%;
      width: 100px;
      background-color: black;
      border: none;
      cursor: pointer;

      &:hover, &:focus {
         outline: none; 

         .arrow {
            fill: #4FD3E8;
            transition: fill 100ms ease-in;
         }
      }
   }

   .arrow {
      fill:#d2d6df;
      height: 50%;
      width: 50%;
   }

   .arrow-right {
      transform: rotate(180deg);
   }

   .close-btn {
      position: absolute;
      top: 0.5rem;
      right: calc(-5vw - 0.5rem);
      z-index: 100;
      background: black;
      border-radius: 100%;
      border: 1px solid #d2d6df;
      padding: 0.5rem;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      width: 30px;
      height: 30px;

      &:hover, &:focus {
         transform: scale(1.2);
         border-color: #d36c6c;
         outline: none;
         transition: transform 100ms ease-in;
         transition: border-color 100ms ease-in;

         svg {
            fill: #d36c6c;
            transition: fill 100ms ease-in;
         }
      }

      svg {
         width: 100%;
         height: 100%;
         fill: #d2d6df;
      }
   }

   @media(max-width: 700px) {
      #light-box {
         .lightbox-content {
            padding: 2rem;
         }

         .controls-left, .controls-right {
            top: auto;
            bottom: -2.25rem;
            width: 50%;
         }

         .controls-left {
            left: 0;
            justify-content: flex-end;
         }

         .controls-right {
            right: 0;
            justify-content: flex-start;
         }

         .previous-btn, .next-btn {
            border: 1px solid #cbcbcb;
            border-radius: 3px;
            padding: 0.5rem;
            width: 70px;
         }

         .close-btn {
            position: fixed;
            width: 35px;
            height: 35px;
            top: 0.5rem;
            left: 0.5rem;
         }
      }
   }

   @media(max-width: 700px) and (orientation: portrait) {
      #light-box {
         padding: 2rem 0;

         .lightbox-content {
            padding: 2rem 0;
         }

         .controls-left, .controls-right {
            bottom: -1.25rem;
         }

         // .close-btn {
         //    top: 0.5rem;
         //    left: 0.5rem;
         // }
      }
   }

   @media(max-width: 700px) and (orientation: landscape) {
      #light-box {
         .lightbox-content {
            margin-bottom: 1rem;
            padding: 1rem 0;
         }

         .controls-left, .controls-right {
            bottom: -2.25rem;
         }

         // .close-btn {
         //    top: 0;
         // }
         
         img {
            max-height: 65vh;
         }
      }
   }
</style>