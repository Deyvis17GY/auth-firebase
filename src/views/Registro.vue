<template>
  <h1 class="my-5">Registro de Usuarios</h1>
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
      >
      <input type="password" 
      placeholder="repita contraseña"
      class="form-control my-2"
      v-model.trim="pass2"
      >
      <button type="submit"
      class="btn btn-primary w-100"
      :disabled="bloquear"
      >
          Registrar
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
            pass2:''
        }
    },
    computed: {
        bloquear(){
            if(!this.email.includes('@')){
                return true
            }
            if(this.pass1.length > 5 && this.pass1 === this.pass2){
                return false
            }
            return true
        },
        ...mapState(['error'])
    },
    methods: {
        ...mapActions(['registrarUsuario']),
        async procesarForm(){
            await this.registrarUsuario({email:this.email,password:this.pass1})
             if(this.error.tipo !== null){
                return
            }
            this.email = ''
            this.pass1 = ''
            this.pass2 = ''
        }
    },
}
</script>

<style>

</style>