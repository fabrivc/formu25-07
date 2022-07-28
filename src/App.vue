<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logonuevo.png" >
    <Formu @emit-agregar-usuario="addUsuarioTabla"/>
    <div v-if="muestroTabla">
    <button  class="btn btn-secondary btn-lg mb-2" @click="verTabla" @emitVerTabla="muestroTabla">Cerrar tabla de registros</button>
    <Tablaformu :usuarios="usuarios" />
    </div>
  </div>
</template>

<script>
import Formu from './components/Formu.vue'
import Tablaformu from './components/Tablaformu.vue'

export default {
  name: 'App',
  components: {
   Formu,Tablaformu
  },
  data() {
        return {
          selected: null,
            usuarios: [],
            
        }
    },
        addUsuarioTabla(usuario) {
            console.log(usuario);
            const nuevoUsuario = {...usuario};
            this.usuarios.push(nuevoUsuario);
        },
        
    }

</script>

<style scoped>
#app {
  background:
  #E8C39A;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #78450C;
  margin-top: 3px;
  margin-bottom: 0px;
}
.imglogo{
  size: 300px;
}
</style>
