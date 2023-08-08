<template>
  <div id="ListaComponent">
    <h1>Lista Cursos</h1>
    <div id="contenedor">
                <div id="cards" class="container" v-for="curso in consultarNoCompletados" v-bind:key="curso.id">
                <b-card id="imagen"
                    v-bind:title="curso.nombre"
                    v-bind:img-src="curso.img"
                    img-alt="Image"
                    img-top
                    tag="article"
                    style="max-width: 20rem;"
                    class="mb-2"
                ><br>
                    <b-card-text id="textoCard">
                        <div class="container">
                            <div class="row"> 
                                <h4>Informacion</h4>
                                <div class="col-md-2" id="circulos">
                                    <div class="linea"><span class="circulitoUno"></span></div> 
                                    <div class="linea"><span class="circulitoDos"></span></div>
                                    <div class="linea"><span class="circulitoUno"></span></div>
                                    <div class="linea"><span class="circulitoDos"></span></div>
                                    
                                </div>
                                <div class="col-md-10">
                                    <p>Costo: <strong>${{ curso.costo }}</strong></p>
                                    <p>Duracion: {{ curso.duracion }}</p>                   
                                    <p>Cupos: <strong>{{ curso.cupos }}</strong></p><p>Completado: {{ curso.completado }}</p>                            
                                    <p>Fecha de registro:</p>
                                    <p>{{ curso.fecha_registro}}</p>
                                    <p>Descripcion: {{ curso.descripcion }}</p>
                                </div>
                            </div>
                        </div>
                    </b-card-text> 
                </b-card>
            </div>
        </div>
  </div>
</template>

<script>
import { mapState,mapActions, mapGetters } from 'vuex';
export default {
  name: 'ListaComponent',
  props: {
    titulo: String
  },
  data:function(){
    return{

    }
  },
  methods:{
    ...mapActions('informacion_curso',['consultarCursos']),
  },
  computed:{
    ...mapState('informacion_curso',['datos']),
    ...mapGetters('informacion_curso',['consultarNoCompletados']),
  },
  watch:{},
  created(){
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#contenedor{
    padding: 100px 100px;
   display: flex;


}
#cards{
    width: 350px;
   
}
b-card{
    border: solid 1px grey;
}
#textoCard{
    text-align: start;
}
img-src{
    width: 50%;
}
#circulos{
    flex-direction: column;
    display: flex;
}
.circulitoUno{
    align-items: start;
    float: left;
    width: 40px;
    height: 40px;
    border-radius: 50%; 
    background-color: rgb(154, 91, 213);
}
.circulitoDos{
    align-items: start;
    float: left;
    width: 40px;
    height: 40px;
    border-radius: 50%; 
    background-color: rgb(54, 119, 38);
}
.linea {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #ccc;
    height: 100%;
    width: 3px;
}
h1{
    padding: 100px 0px;
    font-weight: 800;
    background-color:#2ecc71 ;
    color: #fff;
  }
</style>
