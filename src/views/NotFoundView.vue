<template>
    <div id="NotFoundView">
      <h1>Pagina no Encontrada</h1>
        <p>Disculpe las Molestias</p>
        <router-Link to="/">Volver a Home</router-Link>
    </div>
  </template>
  
  <script>
  export default {
    name: 'NotFoundView',
    props: {
    },
    data:function(){
      return{
  
      }
    },
    methods:{
    },
    computed:{
    },
    watch:{},
    created(){
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  #NotFoundView{
    background-color: chartreuse;
    font-size: 35px;
    color: black;
    margin: 2%;
  }
  
  </style>
  