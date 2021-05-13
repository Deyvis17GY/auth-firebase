<template>
  <input type="text" 
    class="form-control my-2" 
    placeholder="Ingresa nombre"
    v-model.trim="tarea.nombre"
    >
    <div class="form-check form-check-inline">
      <input class="form-check-input" type="checkbox" id="chk-1" 
      v-model="tarea.categorias" value="javascript">
      <label class="form-check-label" for="chk-1">Javascript</label>
    </div>

    <div class="form-check form-check-inline">
      <input class="form-check-input" type="checkbox" id="chk-2" 
      v-model="tarea.categorias" value="node js">
      <label class="form-check-label" for="chk-2">Node.js</label>
    </div>

    <div class="mt-2">
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="rd-1"
        value="urgente" v-model="tarea.estado">
        <label class="form-check-label" for="rd-1">Urgente</label>
      </div>
       <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="rd-2"
        value="relax" v-model="tarea.estado">
        <label class="form-check-label" for="rd-2">Relax</label>
      </div>
    </div>

    <div class="mt-2">
      <input class="form-control" type="number" v-model.number="tarea.numero">
    </div>

    <button class="btn btn-primary mt-3" 
    type="submit" :disabled="bloquear">Procesar</button>
</template>

<script>
export default {
    props:{
        tarea:Object
    },
    computed: {
       bloquear(){
       return this.tarea.nombre.trim()===""? true :false
       }
    }
}
</script>

<style>

</style>