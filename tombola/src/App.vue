<template>
  <div id="app">
    <img src="./assets/iniser.png" id="logo">


    <h2 v-if="winner" class="winnerTitle">Y el ganador es</h2>
    <div class="premios">
      <img src="./assets/premios.png" alt="">
      <h2><strong> {{ winner }} </strong></h2>
    </div>

    <img v-if="winner" src="./assets/ganador.png" class="ganadorImagen" alt="">

    <button  v-on:click="getwinner">Obtener Ganador!</button>




  </div>
</template>

<script>

import axios from 'axios';
import pickRandom from 'pick-random';
import firebase from 'firebase';

let config = {
  //TU CONFIGURACIÓN
    apiKey: "AIzaSyBlk4XI73nkLAZtwLmnNo5aLwp1OAJivXE",
    authDomain: "tombola-c9919.firebaseapp.com",
    databaseURL: "https://tombola-c9919.firebaseio.com",
    projectId: "tombola-c9919",
    storageBucket: "tombola-c9919.appspot.com",
    messagingSenderId: "98129464472"
}
let app = firebase.initializeApp(config);
let db = app.database();
let fbattendees = db.ref();

export default {
  name: 'app',

  firebase: {
    fbattendees: fbattendees
  },
  mounted() {

  },
  data () {
    return {
      msg: 'Raffle with Vue.js',
      fbattendees: null,
      winner: null
    }
  },
  methods: {

    getwinner: function(){


      this.winner = pickRandom(this.fbattendees, {count:1});
      this.winner = this.winner[0]['Nombre'] + ' ' + this.winner[0]['Apellidos'];
    }
  }


}
</script>

<style>
body,
h1,
h2 {
  margin: 0;
}
.ganadorImagen{
  display: block;
  margin-left: auto;
  margin: auto;
}
.winnerTitle{
  color: white;
  font-weight: 700;
  font-size: 40px;
}
body{
  position: relative;
  background-color: blue;
}
.premios{
  position: relative;
}
.premios h2{
  position: absolute;
  bottom: 52px;
text-align: center;
left: 50%;
transform: translateX(-50%);
font-size: 26px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding-top: 12rem;
  padding-bottom: 2rem;
}
button{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  background-color: #f5a604;
  color: white;
  font-size: 22px;
    border-radius: 4px;
    font-weight: 700;
    border-right: 6px solid #ec8005;
border-bottom: 6px solid #ec8005;
border-top: 0;
border-left: 0;
padding: .5rem 1rem;
}
#logo{
  position: absolute;
  top: 0;
  right: 10%;
  max-width: 20%;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
