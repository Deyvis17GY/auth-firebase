<template>
  <form @submit.prevent="procesarForm">
    <Input :tarea="tarea"/>
  </form>
  <hr>
  <ListaTarea/>

</template>

<script>
import Input from '../components/Input'
import ListaTarea from '../components/ListaTarea'
import {mapActions} from 'vuex'
const shortid = require('shortid')

export default {
  name: 'Home',
  components: {
    Input,
    ListaTarea
  },
  data() {
    return {
      tarea:{
        id:'',
        nombre:'',
        categorias:[],
        estado:'',
        numero:0
      }
    }
  },
  methods: {
    ...mapActions(['setTareas','cargarLocalStorage']),
    
    procesarForm(){
     
      if(this.tarea.nombre.trim()===''){
        console.log('Campo vacio')
        return
      }
      // generar id
      this.tarea.id = shortid.generate()
      
      //Enviar datos
      this.setTareas(this.tarea)

      this.tarea =  {
        id:'',
        nombre:'',
        categorias:[],
        estado:'',
        numero:0
      }
    }
  },
   created() {
    this.cargarLocalStorage()
  },
  
}
</script>
