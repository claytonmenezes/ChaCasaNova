<template>
    <div class="grid grid-cols-6 sepia">
      <div v-for="(photo, index) in photos" :key="index" class="photo col-span-3" :style="getRandomStyles()" >
        <img :src="photo" alt="Foto" class="photo-image">
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MuralDeFotos',
    props: {
      photos: {
        type: Array,
        required: true
      }
    },
    methods: {
      getRandomStyles() {
        const rotation = Math.floor(Math.random() * 20 - 10)
        const top = Math.floor(Math.random() * 30)
        const left = Math.floor(Math.random() * 30)
        return {
          transform: `rotate(${rotation}deg)`,
          top: `${top}px`,
          left: `${left}px`
        };
      }
    }
  };
  </script>
  
  <style scoped>  
  .photo {
    box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.3);
    border-radius: 8px;
    overflow: hidden;
    background: white;
    transition: transform 0.2s ease;
  }
  
  .photo-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  </style>
  