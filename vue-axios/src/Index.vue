<template>
<div id="app">
<header>
<span>Basic Ajax Request with Axios in Vue</span>
</header>
<main>
<h2>Click the button to get 10 Chuck Norris Random jokes</h2>
<button id="btn" class="" v-on:click="getJokes">Get the Jokes</button>

<div v-if="loading">
<img src="../src/assets/loader.gif"/>
Loading.....
</div>

<div class="wrapper">
<div class="row">
<div v-for="joke in jokes" :key="joke.id">
<div class="col-md-4 cards">
<!--Adding image for every joke is optional  -->
<!-- <img src="#" class="img-responsive" alt="images placeholder">  -->
<div>
<h3>Joke no. :   {{ joke.id }}</h3>
<h4> {{ joke.joke }} </h4>
<!-- <h4> {{ joke.categories }} </h4> -->
</div>
</div>
</div>
</div>
</div>
</main>
</div>
</template>

<script>
  import axios from 'axios';
  
export default {
  name: 'app',
  data () {
    return {
      jokes: [],
      loading: false
    }
  }, 
  methods: {
    getJokes: function () {
      this.loading = true;
      axios.get("http://api.icndb.com/jokes/random/10")
      .then((response)  =>  {
        this.loading = false;
        this.jokes = response.data.value;
      }, (error)  =>  {
        this.loading = false;
      })
    }
  },
}
</script>

<style>
  
body {
  margin: 0;
}
#app {
  font-family: 'Open Sans';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #3D5F5E;
}

main {
  text-align: center;
  margin-top: 40px;
}
header {
  margin: 0;
  height: 55px;
  padding: 0 16px 0 25px;
  background-color: #1F4746;
  color: #ffffff;
}
header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: .03em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 18px;
  text-align: center;
}
button {
  background: #1F4746;
  color: #ffffff;
  padding: 15px;
  border-radius: 10px;
  font-weight: bold;
  font-size: 15px;
  border: 0;
}
.cards {
  background: #F5F5F5;
  height:130px;
  column-count: 1;
  column-gap: 5em;
  margin-top: 25px;
}
.cards:hover {
  transform: translateY(-0.5em);
  background: #EBEBEB;
}

</style>
