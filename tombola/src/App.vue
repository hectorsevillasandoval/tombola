<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Attendees: {{ attendees }}</h1>
    <h2>The winner is: <strong> {{ winner }} </strong></h2>
  </div>
</template>

<script>

import axios from 'axios';
import pickRandom from 'pick-random';
import firebase from 'firebase';

export default {
  name: 'app',
  mounted() {
    this.getWinner();
  },
  data () {
    return {
      msg: 'Raffle with Vue.js',
      attendees: [
        'Hector',
        'Rikkert',
        'Jeykel',
        'Francisco',
        'Dratzen'
      ],
    winner: null
    }
  },
  methods: {
    getAttendees(){
      /*axios.get(URL)
        .then( (response) => {
          this.attendees = response.data.attendees;
        });*/
      

    },// END GET ATTENDEES
    getWinner(){
      this.winner = pickRandom(this.attendees, {count:1});
    }
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
