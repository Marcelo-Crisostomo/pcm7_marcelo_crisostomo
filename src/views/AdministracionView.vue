<template>
    <div id="AdministracionView">
    <h1>Administración</h1>

        <b-button id="btnAgregar" @click="modalShow = !modalShow">Agregar Curso</b-button><br>
        <TablaComponent></TablaComponent> <br>
        <TotalesComponent></TotalesComponent>

        <!-- MODAL -->
            <div>
              <b-modal v-model="modalShow">
              
                <div>
                    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
                      <b-form-group
                        id="input-group-1"
                        label="Nombre del Curso:"
                        label-for="input-1"                       
                      >
                        <b-form-input
                          id="input-1"
                          v-model="form.nombre"
                          type="text"
                          required
                        ></b-form-input>
                      </b-form-group>

                      <b-form-group 
                        id="input-group-2" 
                        label="URL Imagen del Curso:" 
                        label-for="input-2"
                        >
                        <b-form-input
                          id="input-2"
                          v-model="form.img"
                          required
                        ></b-form-input>
                      </b-form-group>

                      <b-form-group 
                        id="input-group-3" 
                        label="Cupos del Curso:" 
                        label-for="input-3"
                        >
                        <b-form-input
                          id="input-3"
                          type="number"
                          v-model="form.cupos"
                          required
                        ></b-form-input>
                      </b-form-group>

                      <b-form-group 
                        id="input-group-4" 
                        label="Inscritos en el Curso:" 
                        label-for="input-4"
                        >
                        <b-form-input
                          id="input-4"
                          type="number"
                          v-model="form.inscritos"
                          required
                        ></b-form-input>
                      </b-form-group>

                      <b-form-group 
                        id="input-group-5" 
                        label="Duración del Curso:" 
                        label-for="input-5"
                        >
                        <b-form-input
                          id="input-5"
                          v-model="form.duracion"
                          required
                        ></b-form-input>
                      </b-form-group>

                      <b-form-group 
                        id="input-group-6" 
                        label="Fecha de Registro:" 
                        label-for="input-6"
                        >
                        <b-form-input
                          id="input-6"
                          type="date"
                          v-model="form.fecha_registro"
                          required
                        ></b-form-input>
                      </b-form-group>

                      <b-form-group 
                        id="input-group-7" 
                        label="Costo del Curso:" 
                        label-for="input-7"
                        >
                        <b-form-input
                          id="input-7"
                          type="number"
                          v-model="form.costo"
                          required
                        ></b-form-input>
                      </b-form-group>


                      <b-form-textarea
                        id="textarea"
                        v-model="form.descripcion"
                        rows="3"
                        max-rows="6"
                      ></b-form-textarea>
                      <b-button type="submit" variant="primary">Submit</b-button>
                      <b-button type="reset" variant="danger">Reset</b-button>
                    </b-form>
                    <b-card class="mt-3" header="Form Data Result">
                      <pre class="m-0">{{ form }}</pre>
                    </b-card>
                </div>              
              </b-modal>
            </div>
            <!-- FIN MODAL-->
           
    </div>
  </template>
  
  <script>
  import { mapState,mapActions } from 'vuex';
  import TablaComponent from '@/components/TablaComponent.vue';
  import TotalesComponent from '@/components/TotalesComponent.vue';
  export default {
    name: 'AdministracionView',
    props: {
    },
    components:{
      TablaComponent,
      TotalesComponent,
    },
    data:function(){
      return{
        modalShow: false,
        form_tabla: {
          id:'',
          curso: '',
          img: '',
          costo: 0,
          duracion:'',
          cupos:0,
          inscritos:0,
          terminado:false,
          fecha:'',
          descripcion:'',
        },
        form:{
          id:'',
          nombre: '',
          img: '',
          costo: 0,
          duracion:'',
          cupos:0,
          inscritos:0,
          completado:false,
          fecha_registro:'',
          descripcion:'',
        },
        show: true
      }
    },
    methods:{
      ...mapActions('informacion_curso',['registrarDatosCards', 'registrarDatosTabla']),
      onSubmit(event) {
        event.preventDefault();

        if(this.form.inscritos > this.form.cupos){
          alert("LA CANTIDAD DE INSCRITOS NO DEBE SER MAYOR QUE LA CANTIDAD DE CUPOS.INGRESE VALORES CORRECTOS");
        }
        else{
          // funcion para convertir a JSON los datos
          // alert(JSON.stringify(this.form));

          //GENERAMOS EL NUEVO ID
           let indiceultimo = this.datos.length -1;
           let elidultimo = this.datos[indiceultimo].id;
           let nuevoid = elidultimo + 1;

            // clonamos los campos uno a uno con los nombres adecuados
           this.form.id = nuevoid;
           this.form_tabla.id = this.form.id;
           this.form_tabla.curso = this.form.nombre;
           this.form_tabla.img = this.form.img;
           this.form_tabla.costo = this.form.costo;
           this.form_tabla.duracion = this.form.duracion;
           this.form_tabla.cupos = this.form.cupos;
           this.form_tabla.inscritos = this.form.inscritos;
           this.form_tabla.terminado = this.form.completado;
           this.form_tabla.fecha = this.form.fecha_registro;
           this.form_tabla.descripcion= this.form.descripcion;

          let dataCards = {...this.form};
          let dataTabla = {...this.form_tabla}

          this.registrarDatosCards(dataCards);
          this.registrarDatosTabla(dataTabla);


        }


      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
          this.form.nombre='';
          this.form.img='',
          this.form.costo=0;
          this.form.duracion='';
          this.form.cupos=0;
          this.form.inscritos=0;
          this.form.completado=false;
          this.form.fecha_registro='';
          this.form.descripcion='';
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
    },
    computed:{
      ...mapState('informacion_curso',['datos','cursos_no_completados']),
    },
    watch:{},
    created(){
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
 #btnAgregar{
  margin: 50px 0px;
  background-color: #2ecc71;
  border: none;
  padding: 15px 30px;  
  font-weight: 600;
}
#btnAgregar:hover{
  background-color: #27ae60;
}
h1{
  padding: 100px 0px;
  font-weight: 800;
  background-color:#2ecc71 ;
  color: #fff;
}
  </style>
  