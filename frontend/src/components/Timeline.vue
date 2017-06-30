<template>
  <div class="hello">
    <h1>{{ this.utilisateur ? 'Bonjour ' + this.utilisateur + ' ! ' : 'Identifiez-vous !' }}</h1>
    <utilisateurs :utilisateurs="utilisateurs" @userChanged="onChange"/>

    <h1 v-if="loading">Chargement des tweets en cours</h1>
    <div v-else>
        <ul>
          <feed :tweets="tweets" :loading="loading" :utilisateur="utilisateur" @retweeted="retweet"></feed>
        </ul>
    </div>
  </div>
</template>



<script>
import Feed from './Feed'
import Utilisateurs from './Utilisateurs'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'hello',
  components: {Feed, Utilisateurs},
  props: ['utilisateur'],

  created () {
    this.fetchTweets()
    this.fetchUtilisateurs()
  },

  methods: {
    retweet: function (id) {
      var tweet = this.tweets.find(tweet => id === tweet.id)
      tweet.retweeters.push({handle: this.utilisateurs})
    },

    onChange: function (handle) {
      this.utilisateur = handle
    },

    fetchUtilisateurs: function () {
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
        this.utilisateurs = response.body
      }, response => {
        // error callback
      })
    },

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
      loading: true,
      utilisateurs: []
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

</style>
