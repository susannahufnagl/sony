<template>
  <div>
    <header>
      <nav class="navbar navbar-dark bg-dark">
        <a class="navbar-brand" href="#">Bilder zum Downloaden</a>

      </nav>

    </header>
    
  
  <div class="Bildergalerie">

     <div class="row">
      <div class="col-md-4 mb-4" v-for="image in images" :key="image.id">
        <div class="card h-100">
          <img :src="image.download_url" :alt=" 'Picture taken by' + image.author" class="card-img-top">
          <div class="card-body">
          <h5 class="card-title">{{image.author}}</h5>
        </div>
        <div class="card-footer">
          <a :href="image.download_url" class="btn btn-block downloard-btn" download>Download</a>
          </div>

        </div>
      </div>
     </div>
     <!-- class="image-card"
      v-for="image in images" :key="image.id">
      <img :src="image.download_url" :alt="image.author">
      <p>{{ image.author }}</p>
      <button @click="downloadfile">Download</button>
      <a :href="image.download_url" download>download!</a>
     -->
   </div> 
  
  <footer>
    <div class="footer">
      <a href="https://www.linkedin.com/in/susanna-hufnagl-ba5321213/" target="_blank">
        <i class="fab fa-linkedin fa-xs"></i>
    </a>
  </div>
  </footer>
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
/* methods: {
    downloadfile() {

      let downloadlink = document.createElement("a")
      downloadlink.href = images;
      downloadlink.download = src="image.download_url";
      downloadlink.style.display = 'none';
      document.body.appendChild(downloadlink);
      downloadlink.click();
      document.body.removeChild(downloadlink);
    }


}
*/

  
  
}
</script>
<style scoped>
body {
  background: black;
  color: white;
  font-family: 'Helvetica Neue', sans-serif;
}



.Bildergalerie {
  display: grid;
  grid-template-columns: repeat(auto-fill, minimax(100px,1fr));
  margin-bottom: 50px;
}
.card {

  overflow: hidden;
  margin: 10px;
  border-radius: 10px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;


}
.card:hover{
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.card-img-top{
  transition: transform .3s ease-in-out, filter .3s ease-in-out;
  border-radius: 10px 10px 0 0;
  
}
.card:hover .card-img-top{
  transform: scale(1.05);
  filter: brightness(110%);
}
.download-btn {
  background-color: black;
  color: white;
}
.download-btn:hover {
  display: inline-block;
  font-size: 16px;
  color: white;
  background-color: #0007;
  padding: 10px 20px;
  margin: 10px 0;
  border:none;
  text-decoration: none;
  transition: background-color 0.3s;
}
.download-btn:hover{
  background-color: darkslategrey;
}

footer .footer{
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: rgb(255, 255, 255);
  color: white;
  text-align: center;
  padding: 20px 0;

}
footer a{
  color: white;
  transition:color 0.3s
}
footer a:hover{
  color: #ddd;
}
.fab.fa-linkedin{
  margin-right: 5px;
  color: white;
  

}


</style>
