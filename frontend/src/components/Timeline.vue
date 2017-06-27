<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1 v-if="loading">Chargement des tweets en cours</h1>
    <ul v-else>
        <feed :tweets="tweets" :loading="loading"></feed>
    </ul>

  </div>
</template>



<script>
import Feed from './Feed'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'hello',
  components: {Feed},

  created () {
    this.fetchTweets()
  },

  methods: {
    fetchTweets: function () {
      // GET /someUrl
      this.$http.get('http://localhost:8080/list').then(response => {
        // get body data
        this.tweets = response.body
        this.loading = false
      }, response => {
        // error callback
      })
    }
  },

  data () {
    return {
      tweets: [],
      loading: true
    }
  }
}
</script>




<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}
</style>
