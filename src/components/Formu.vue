<template>
  <div class="app">
    <div class="row">
        <div class="col-12 d-flex justify-content-center">
            <form>
            <div class="col-md-12 mb-2">
              <label class="form-label" for="nombre">Nombre y Apellido</label>
               <p class="form-label">El nombre y apellido debe ser mayor a 10 caracteres y menor de 35</p>
              <input type="text" minlength="10" maxlength="35" id="nombre" class="form-control" @keyup="validarNombre" v-model="usuario.nombre">
            </div>
             <div class="col-md-12 mb-2" v-if='mensajeNombre != ""'>
                <p class="errorForm">{{ mensajeNombre }}</p>
            </div>
            <div class="col-md-12 mb-2">
              <label class="form-label" for="mail">Mail</label>
              <input type="text" id="mail" class="form-control" @keyup="validarMail" v-model="usuario.email">
            </div>
            <div class="col-md-12 mb-2" v-if='mensajeMail != ""'>
                <p class="errorForm">{{ mensajeMail }}</p>
            </div>
            <div class="col-md-12 mb-2">
              <label class="form-label" for="edad">Edad</label>
              <p class="form-label">Debes ser mayor de 18 años!</p>
              <p class="form-label"></p>
              <input  class="form-control" @keyup="validarEdad" v-model="usuario.edad">
            </div>
            <div class="col-md-12 mb-2" v-if='mensajeEdad != ""'>
                <p class="errorForm">{{ mensajeEdad }}</p>
            </div>
            <div class="col-md-12 mb-2">
              <label class="form-label" for="password">Contraseña</label>
              <p class="form-label">Incluir una mayúscula, un caracter especial (!#$..) y un número</p>
              <p class="form-label">La contraseña debe ser de 5 caracteres como minimo y 10 como maximo respetando los parametros anteriores</p>
              <input type="password" minlength="5" maxlength="10" class="form-control" @keyup="validarPassword" v-model="usuario.password">
            </div>
             <div class="col-md-12 mb-2" v-if='mensajePassword != ""'>
                <p class="errorForm">{{ mensajePassword }}</p>
            </div>
            <div class="col-md-12 mb-2">
              <br>
                <input type="button" class="btn btn-secondary btn-lg mb-2" value="Registrar" @click="addUsuario"/>
            </div>
           
            
            </form>
    </div>
  </div>
 </div>
</template>

<script>
export default {
  name: 'Formulario',
    data() {
        return {
            usuario: {
                nombre: "",
                email: "",
                edad: "",
                password: "",
            },
            mensajeNombre: "",
            mensajeMail: "",
            mensajeEdad: "",
            mensajePassword: "",
        }
    },
    methods: {
        verTabla(payload){
                this.$emit("emitVerTabla" , payload)
        },
        addUsuario() {
            if (this.checkForm()){
                this.$emit('emit-agregar-usuario', this.usuario);
                this.usuario.nombre = "";
                this.usuario.email = "";
                this.usuario.edad = "";
                this.usuario.password = "";
            } else {
                alert("Debes llenar todos los campos!");
            }
        },
        checkForm () {
            return (this.validarNombre() && this.validarMail() && this.validarEdad() && this.validarPassword())
            },
        validarNombre(){
            let regex1 = /^[a-zA-Z ]*$/
            if (regex1.test(this.usuario.nombre)){
                this.mensajeNombre = "Nombre valido";
                return true;
            } else {
                this.mensajeNombre = "Nombre inválido";
                return false;
            }
        },
        validarMail(){
            let regex2 =/^[-\w.%+]{1,64}@(?:[A-Z0-9-]{1,63}\.){1,125}[A-Z]{2,63}$/i
            if (regex2.test(this.usuario.email)){
                this.mensajeMail = "";
                return true;
            } else {
                this.mensajeMail = "Email inválido";
                return false;
            }
        },
        validarEdad(){
            if (this.usuario.edad >= 18 && this.usuario.edad <=100){
                this.mensajeEdad = "Edad valida, eres mayor de 18 años!";
                return true;
            } else {
                this.mensajeEdad = "Edad inválida, eres menor de 18 años o mayor de 100!";
                return false;
            }
        },
        validarPassword(){
            let regex3 = new RegExp("^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#\$%\^&\*])(?=.{8,})");
            if (regex3.test(this.usuario.password)){
                this.mensajePassword = "";
                return true;
            } else {
                this.mensajePassword = "Clave inválida"
                return false;
            }
        }
    }
}
</script>


<style scoped>
.app {
    background:#E8C39A;
    
}
.errorForm{
    color:white;
    font-size: 20px;
}

</style>
