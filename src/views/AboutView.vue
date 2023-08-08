<template>
  <div class="about">
    <div>
      <h1>Cursos</h1>
      <div class="container">
        <div class="" id="parrafo">
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure enim magnam, soluta reprehenderit est nam maiores qui hic, maxime laboriosam officiis, facilis velit dignissimos accusantium ducimus harum illo suscipit labore.
      Suscipit vitae, eligendi atque quaerat enim nulla, ipsum excepturi voluptatibus aspernatur, possimus perspiciatis? Praesentium repellendus ratione voluptatum ipsa cumque, voluptatibus commodi temporibus quibusdam illo alias ducimus magnam cupiditate adipisci cum.
      Neque rem assumenda asperiores! Odio odit quis eum cumque, accusamus nam iste recusandae! Libero praesentium atque, nihil deserunt quas quisquam iste, dolore dolores a incidunt ipsa odit iure voluptate quo?</p>
        </div>
              <div id="carrusel">
            <b-carousel
            id="carousel-1"
            v-model="slide"
            :interval="4000"
            controls
            indicators
            background="#ababab"
            img-width="1024"
            img-height="480"
            style="text-shadow: 1px 1px 2px #333;"
            @sliding-start="onSlideStart"
            @sliding-end="onSlideEnd"
            >
            <!-- Text slides with image -->
           

            <!-- Slides with custom text -->
            <b-carousel-slide 
                class="d-block img-fluid w-100"
                width="1024"
                height="480"
                img-src="https://images.unsplash.com/photo-1650297878614-a0eba8ba70ae?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3270&q=80">
                
            </b-carousel-slide>

            <!-- Slides with image only -->
            <b-carousel-slide 
                class="d-block img-fluid w-100"
                width="1024"
                height="480"
                img-src="https://images.unsplash.com/photo-1650297872002-81441fe6373f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3270&q=80">

            </b-carousel-slide>

            <!-- Slides with img slot -->
            <!-- Note the classes .d-block and .img-fluid to prevent browser default image alignment -->
            <b-carousel-slide>
                <template #img>
                <img
                    class="d-block img-fluid w-100"
                    width="1024"
                    height="480"
                    src="https://images.unsplash.com/photo-1650297884022-d10d81c7cd1e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3270&q=80"
                    alt="image slot">
                </template>
            </b-carousel-slide>

            <!-- Slide with blank fluid image to maintain slide aspect ratio -->
            
            </b-carousel>
        </div>
      </div>
    </div>
   
  </div>
</template>
<script>
  export default {
    data() {
      return {
        slide: 0,
        sliding: null
      }
    },
    methods: {
      onSlideStart(slide) {
        this.sliding = true
      },
      onSlideEnd(slide) {
        this.sliding = false
      }
    }
  }
</script>
<style scoped>
#parrafo{
  width: 100%;
  color: cornsilk;
  text-align: justify;
}
#carrusel{
  width: 100%;
  margin-bottom: 50px;
  
}
h1{
  padding: 100px 0px;
  font-weight: 800;
  background-color:#2ecc71 ;
  color: #fff;
}
p{
  padding: 50px 0px;
  text-align: left;
  color:black
}
</style>
