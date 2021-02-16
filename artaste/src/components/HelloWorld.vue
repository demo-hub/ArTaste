<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <md-autocomplete v-model="value" :md-options="movies" @md-changed="getMovies" @md-opened="getMovies">
      <label>Movie</label>

      <template slot="md-autocomplete-item" slot-scope="{ item }">
        <span><img :src="`https://image.tmdb.org/t/p/w500${item.poster_path}`" style="max-width: 50px; padding-right: 0.7em">{{ item.title }}</span>
        </template>
    </md-autocomplete>
  </div>
</template>

<script>
import axios from 'axios'
import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'

/* import Arweave from 'arweave/web';

const arweave = Arweave.init({
  host: '46.101.45.117',
  port: 1984,
  protocol: 'http',
  timeout: 20000,
  logging: false,
});

arweave.wallets.getBalance('MlV6DeOtRmakDOf6vgOBlif795tcWimgyPsYYNQ8q1Y').then(balance => console.log(balance)) */

Vue.use(VueMaterial)

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      value: null,
      movies: []
    }
  },
  methods: {
    getMovies (searchTerm) {
      if (searchTerm) {
        axios
        .get(`https://api.themoviedb.org/3/search/movie?api_key=910de9dfb6ee354720ea90b86866c272&language=en-US&query=${searchTerm}&page=1&include_adult=false`)
        .then(response => {
          this.movies = response.data.results
        })
      }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
.md-input {
  margin-left: 100px !important;
}
</style>
