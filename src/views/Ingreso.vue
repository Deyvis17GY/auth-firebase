<template>
  <h1 class="my-5">Ingreso de Usuarios</h1>
  <div class="alert alert-danger text-center"
  v-if="error.tipo !==null"
  >
      {{error.mensaje}}
  </div>
  <form @submit.prevent="procesarForm">
      <input type="email" 
      placeholder="email"
      class="form-control my-2"
      v-model.trim="email"
      :class="[error.tipo === 'email' ? 'is-invalid' : '']"
      >
      <input type="password" 
      placeholder="contraseña"
      class="form-control my-2"
      v-model.trim="pass1"
      :class="[error.tipo === 'password' ? 'is-invalid' : '']"
      >
      <button type="submit"
      class="btn btn-primary w-100"
      :disabled="bloquear"
      >
          Ingresar
      </button>
  </form>
</template>

<script>
import { mapActions, mapState } from 'vuex'
export default {
    data() {
        return {
            email:'',
            pass1:'',
        }
    },
    computed: {
        bloquear(){
            if(!this.email.includes('@')){
                return true
            }
            if(this.pass1.length > 5){
                return false
            }
            return true
        },
        ...mapState(['error'])
    },
    methods: {
        ...mapActions(['ingresoUsuario']),
        async procesarForm(){
            await this.ingresoUsuario({email:this.email,password:this.pass1})
            if(this.error.tipo !== null){
                return
            }
            this.email = ''
            this.pass1 = ''
        }
    },
}
</script>

<style>

</style>