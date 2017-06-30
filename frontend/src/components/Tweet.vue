<template>
  <div class="tweet">
      <div class="auteur"> <strong>{{ tweet.auteur.prenom }} {{ tweet.auteur.nom }}</strong>
        <i><span class="handle">@{{ tweet.auteur.handle }}</span></i> - {{ moment(tweet.date).fromNow() }}</div>
      <div class="contenu">{{ tweet.contenu }} </div>

      <div class="icons">
        <ul>
          <li class="button"> <icon name="reply"/> </li>

          <li class="button" v-if="retweetable()">
            <a @click="retweet()">
              <icon name="retweet"/>
               <span> {{ tweet.retweeters.length }} </span>
            </a>
          </li>

          <li class="button" v-else>
            <icon name="retweet"/>
            <span> {{ tweet.retweeters.length }} </span>
          </li>

          <li class="button"> <icon name="heart"/> </li>
          <li class="button"> <icon name="envelope"/> </li>
        </ul>
      </div>
  </div>
</template>


<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'
import moment from 'moment'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'tweet',
  props: ['tweet', 'utilisateur'],
  components: {Icon},

  methods: {
    moment: function (date) {
      return moment(date)
    },

    retweetable: function () {
      if (this.tweet.auteur.handle === this.utilisateur) {
        return false
      }
      return true
    },

    retweet: function () {
      this.$http.get('http://localhost:8080/retweet', {params: {utilisateur: this.utilisateur, tweet: this.tweet.id}, responseType: 'text'}).then(response => {
        this.tweets = response.body
        this.loading = false
        this.$emit('retweeted', this.tweet.id)
      }, response => {
         // error callback
      })
    }

  },
  created () {
    moment.locale('fr')
  }

}
</script>

<style scoped>
li.button {
 display: inline-block;
}

a {
 color: #42b983;
}

span.handle {
 color: gray;
}
</style>
