<template>
  <div id="app">
    <nav class="shadow">
      <div>
        <b-navbar toggleable="lg" type="dark" id="barraNav">
          <b-navbar-brand href="#">CURSOS ALFAWEB</b-navbar-brand>
          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
          <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
              <b-nav-item href="#"><router-link to="/about">About</router-link></b-nav-item>
              <b-nav-item href="#"><router-link to="/"><i class="fa-solid fa-house"></i></router-link></b-nav-item>
              <b-nav-item href="#"><router-link to="/administracion"><i class="fa-solid fa-screwdriver-wrench"></i></router-link></b-nav-item>
            </b-navbar-nav>
          </b-collapse>
        </b-navbar>
      </div>      
    </nav>
    <router-view/>
  </div>
</template>
<script>
import { mapActions } from 'vuex';

export default{
  name:'App',
  data: function(){
    return{

    }
  },
  props:{

  },
  components:{
    
  },
  methods:{
    ...mapActions('informacion_curso',['consultarCursos', 'consultarDatosTabla']),
  },
  computed:{

  },
  watch:{

  },
  beforeMount(){
    this.consultarCursos();
    this.consultarDatosTabla();
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap');
#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h1{
  padding: 100px 0px;
  font-weight: 800;
  background-color:#2ecc71 ;
  color: #fff;
}
nav a {
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  padding: 0px 20px;
}

nav a.router-link-exact-active {
  color: #f1c40f;
}
#barraNav{
  background-color: #8e44ad;
  padding: 10px 20px;
}
</style>
