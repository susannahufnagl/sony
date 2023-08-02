<template>
  <div class="Bildergalerie">
     <div 
      class="image-card"
      v-for="image in images" :key="image.id">
      <img :src="image.download_url" :alt="image.author">
      <p>{{ image.author }}</p>
      <a :href="image.download_url" download>Download</a>
      
     </div>

  </div> 
</template>

<script>
export default {
  async asyncData({ $axios}){
    const images= await $axios.$get('https://picsum.photos/v2/list?limit=50')
    return {images}
  },
  head() {
    return {
      title: "Images",
      meta: [{ hid: 'description', name: 'description' },
    ],
    }
  },
  
  
}
</script>
<style scoped>
.Bildergalerie {
  display: grid;
  grid-template-columns: repeat(auto-fill, minimal(200px,1fr));
}
.image-card {
  overflow: hidden;

}
.image-card img{
  width:100%;
  transition: transform .3s ease-in-out;
}
.image-card:hover img{
  transform: scale(1.1);
}
</style>
