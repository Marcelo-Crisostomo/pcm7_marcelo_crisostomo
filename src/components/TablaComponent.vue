<template>
    <div id="TablaComponent" class="container">     
        <div class="container">
            <!-- <b-table striped hover :items="datos"></b-table>4 -->
            <table class="table">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th >Nombre</th>
                        <th >Cupos</th>
                        <th >Inscritos</th>
                        <th >Duracion</th>
                        <th >Costo</th>
                        <th >Completado</th>
                        <th >Fecha Registro</th>
                        <th >Acciones</th>                     
                    </tr>
                    <tr v-for="dato in datos_tabla" v-bind:key="dato.id">
                      <td>{{ dato.id }}</td>
                      <td><strong>{{  dato.curso }}</strong></td>
                      <td>{{  dato.cupos }}</td>
                      <td>{{  dato.inscritos }}</td>
                      <td>{{  dato.duracion }}</td>
                      <td>${{  dato.costo }}</td>
                      <td>{{  dato.terminado }}</td>
                      <td>{{  dato.fecha }}</td>
                        <td>
                            <button id="editar" class="btn" v-on:click.prevent="activarEditar(dato.id)" ><i class="fas fa-edit"></i></button>
                            <button id="eliminar" class="btn" v-on:click.prevent="eliminar(dato.id)"><i class="fas fa-trash"></i></button>
                        </td>
                    </tr>
                </thead>
            </table>           
        </div>
        <!-- MODAL -->
        <div>
              <b-modal v-model="modalShow">             
                <div>
                    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
                       <!--Caja 1 texto-->
                      <b-form-group
                        id="input-group-1"
                        label="Nombre del Curso:"
                        label-for="input-1"
                      >
                        <b-form-input
                          id="input-1"
                          v-model="form.nombre"
                          type="text"
                          placeholder="Ingrese Nombre"
                          required
                        ></b-form-input>
                      </b-form-group>
                      <!--Caja 2 texto-->
                      <b-form-group 
                        id="input-group-2" 
                        label="URL Imagen del Curso:" 
                        label-for="input-2">
                         
                        <b-form-input
                          id="input-2"
                          v-model="form.img"
                          placeholder="Ingrese URL imagen"
                          required
                        ></b-form-input>
                      </b-form-group>
                      <!--Caja 3 texto-->
                      <b-form-group 
                        id="input-group-3" 
                        label="Cupos del Curso:" 
                        label-for="input-3">
                        <b-form-input
                          id="input-3"
                          type="number"
                          v-model="form.cupos"
                          placeholder="Ingrese cupos"
                          required
                        ></b-form-input>
                      </b-form-group>
                       <!--Caja 4 texto-->
                      <b-form-group 
                        id="input-group-4" 
                        label="Inscritos en el Curso:" 
                        label-for="input-4"
                        >
                        <b-form-input
                          id="input-4"
                          type="number"
                          v-model="form.inscritos"
                          placeholder="Ingrese inscritos"
                          required
                        ></b-form-input>                        
                      </b-form-group>
                        <!--Caja 5 texto-->
                      <b-form-group 
                        id="input-group-5" 
                        label="Duración del Curso:" 
                        label-for="input-5"
                        >
                        <b-form-input
                          id="input-5"
                          v-model="form.duracion"
                          placeholder="Ingrese duración"
                          required
                        ></b-form-input>
                      </b-form-group>
                       <!--Caja 6 texto-->
                      <b-form-group 
                        id="input-group-6" 
                        label="Fecha de Registro:" 
                        label-for="input-6"
                        >
                        <b-form-input
                          id="input-6"
                          type="text"
                          v-model="form.fecha_registro"
                          placeholder="Ingrese fecha de registro"
                          required
                        ></b-form-input>
                      </b-form-group>
                       <!--Caja 7 texto-->
                      <b-form-group 
                        id="input-group-7" 
                        label="Costo del Curso:" 
                        label-for="input-7"
                        >
                        <b-form-input
                          id="input-7"
                          type="number"
                          v-model="form.costo"
                          placeholder="Ingrese costo"
                          required
                        ></b-form-input>
                      </b-form-group>
                       <!--Caja 8 textArea-->
                      <b-form-textarea
                        id="textarea"
                        v-model="form.descripcion"
                        placeholder="Descripción del Curso"
                        rows="3"
                        max-rows="6"
                      ></b-form-textarea>
                      <b-button type="submit" variant="warning">Cambiar Info</b-button>
                      <b-button type="reset" variant="danger">Reset</b-button>
                    </b-form>
                    <b-card class="mt-3" header="Form Data Result">
                      <pre class="m-0">{{ form }}</pre>
                    </b-card>
                </div>                       
              </b-modal>
            </div>
    </div>
  </template>
  
  <script>
  import { mapState,mapActions } from 'vuex';
  export default {
    name: 'TablaComponent',
    props: {
    },
    data:function(){
      return{
        prueba: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { age: 38, first_name: 'Jami', last_name: 'Carney' }
        ],
        modalShow: false,
        form: {
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
        show: true,
        mostrarTabla : true,
      }
    },
    methods:{
      ...mapActions('informacion_curso',['consultarDatosTabla', 'eliminarCurso', 'consultarCursosEditarCard', 'consultarCursosEditarTabla', 'editarDatosCard', 'editarDatosTabla']),
      eliminar:function(elid){
        
        let respuesta= confirm('¿Está seguro que desea eliminar el curso?');
          if(respuesta==true){
              this.eliminarCurso(elid);
          }    
      },
      onSubmit(event) {
        event.preventDefault();
        // llamamos al action que realizará la edición con los datos del modelo de datos
          this.$nextTick(() => {
          this.editarDatosCard(this.form);
        });
          this.form_tabla.id=this.form.id;
          this.form_tabla.curso=this.form.nombre;
          this.form_tabla.img=this.form.img;
          this.form_tabla.costo=this.form.costo;
          this.form_tabla.duracion=this.form.duracion;
          this.form_tabla.cupos=this.form.cupos
          this.form_tabla.inscritos=this.form.inscritos;
          this.form_tabla.terminado=this.form.completado;
          this.form_tabla.fecha=this.form.fecha_registro;
          this.form_tabla.descripcion=this.form.descripcion;
          this.$nextTick(() => {
          
          this.editarDatosTabla(this.form_tabla);
        })
        // mostramos la tabla con los cambios
          this.$nextTick(() => {
          this.mostrarTabla= true
          })
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
        
          this.show = false
          this.$nextTick(() => {
            this.show = true
          })
      },

      activarEditar(unid){
 
        //ocultamos la tabla para hacer cambios
        this.$nextTick(() => {
          this.mostrarTabla = false;
        })
        // consultamos el curso de acuerdo al id para poblar el state this.curso_editar
        this.consultarCursosEditarCard(unid);
        this.consultarCursosEditarTabla(unid);
        this.modalShow = true;
        // asignamos el id manualmente al objeto del modelo de datos
        this.form.id = unid;
          // asignamos manualmente al objeto del modelo de datos los valores recuperados del state
          this.form.nombre=this.curso_editar_card.nombre;
          this.form.img=this.curso_editar_card.img;
          this.form.costo=this.curso_editar_card.costo;
          this.form.duracion=this.curso_editar_card.duracion;
          this.form.cupos=this.curso_editar_card.cupos;
          this.form.inscritos=this.curso_editar_card.inscritos;
          this.form.completado=this.curso_editar_card.completado;
          this.form.fecha_registro=this.curso_editar_card.fecha_registro;
          this.form.descripcion=this.curso_editar_card.descripcion;
      },    

    },
    computed:{
      ...mapState('informacion_curso',['datos_tabla', 'curso_editar_card', 'curso_editar_tabla']),
    },
    watch:{},
    created(){
       //  this.consultarCursos();
        // this.consultarDatosTabla();
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
#eliminar{
    color: red;
}
#editar{
    color:rgb(236, 213, 44);
}
label{
  font-weight: bolder;
}
  
  </style>
  