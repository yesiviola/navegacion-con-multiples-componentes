<template>
  <div id="app" class='m-2' >
    <nav>
      <div class="nav nav-tabs" id="nav-tab" role="tablist">
        <a v-bind:class='"nav-item nav-link "+mostrarInicio' id="inicio" 
          data-toggle="tab" href="#nav-home" role="tab" 
          aria-controls="nav-home" aria-selected="true"
          v-on:click='manejoClick($event)'>Inicio</a>
        <a v-bind:class='"nav-item nav-link "+mostrarPerfil' id="Perfil" 
          data-toggle="tab" href="#nav-profile" role="tab" 
          aria-controls="nav-profile" aria-selected="false"
          v-on:click='manejoClick($event)'>Perfil</a>
         <a v-bind:class='"nav-item nav-link "+mostrarActividades' id="actividades" 
          data-toggle="tab" href="#nav-contact" role="tab" 
          aria-controls="nav-contact" aria-selected="false"
          v-on:click='manejoClick($event)'>Actividades</a>
      </div>
    </nav>
    <div class="tab-content" id="nav-tabContent">
      <div v-bind:class='"tab-pane fade show "+mostrarInicio' id="nav-home" role="tabpanel" 
        aria-labelledby="nav-home-tab">
        <LoginComponente
          v-if='!registro && !logon'
          v-on:eventoRegistro='activarRegistro'
          v-on:ingresoCorrecto='ingreso'
          v-bind:estadoLogon='logon'
          v-bind:datosPerfil='Perfil'>
        </LoginComponente>
        <RegistroComponente 
          v-if='registro && !logon'
          @cancelarRegistro='quitarRegistro'
          @irInicio='aInicio($event)'>
        </RegistroComponente>
        <InicioComponente
          v-if='logon'
          v-bind:nombreUsuario='PerfilComponente.nombre'></InicioComponente>
        </div>
      <div v-bind:class='"tab-pane fade show "+mostrarPerfil' id="nav-profile" role="tabpanel" 
        aria-labelledby="nav-profile-tab">
        <PerfilComponente
          v-bind:pNombre='Perfil.nombre'
          v-bind:pEmail='Perfil.email'
          v-bind:estadoLogon='logon'
          @actualizarPerfil='actualizarDatos($event)'>
        </PerfilComponente>
      </div>
      <div v-bind:class='"tab-pane fade show "+mostrarActividades' id="nav-contact" role="tabpanel" 
        aria-labelledby="nav-contact-tab">Debe ingresar al Sistema.</div>
    </div>
  </div>
</template>

<script>
 import LoginComponente from './components/LoginComponente.vue'
import RegistroComponente from './components/RegistroComponente.vue'
import InicioComponente from './components/InicioComponente.vue'
import PerfilComponente from './components/PerfilComponente.vue'

export default {
  name: 'app',
  data: function () {
    return {
    logon: false,
    mostrarInicio: 'active',
    mostrarPerfil: '',
    mostrarActividades: '',
    registro:false,
    Perfil : {nombre:'',email:'',pass:''}
  }},
  methods: {
    manejoClick: function (e) {
      if (e.target.id==='Inicio'){
        this.mostrarInicio='active'
        this.mostrarPerfil=''
        this.mostrarActividades=''}
      else if (e.target.id==='Perfil'){
        this.mostrarInicio=''
        this.mostrarPerfil='active'
        this.mostrarActividades=''}
      else 
        {
        this.mostrarInicio=''
        this.mostrarPerfil=''
        this.mostrarActividades='active'}
    },
    activarRegistro: function (){
      this.Registro=true
    },
    quitarRegistro: function (){
      this.Registro=false
    },
    ingreso: function (){
      this.logon= true
      this.mostrarInicio='active'
      this.mostrarPerfil=''
      this.mostrarActividades=''
    },
    aInicio: function (e){
      this.Perfil =e
      this.Registro =false
    },
    actualizarDatos: function (e){
      this.Perfil.nombre=e.nombre
      this.Perfil.email=e.email
    }
  },
   components: {
    LoginComponente,
    RegistroComponente,
    InicioComponente,
    PerfilComponente,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
