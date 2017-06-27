<template>
  <div class="tweet">
      <div class="auteur"> <strong>{{ tweet.auteur.prenom }} {{ tweet.auteur.nom }}</strong> <i><span class="handle">@{{ tweet.auteur.handle }}</span></i> - {{ moment(tweet.date).fromNow() }}</div>
      <div class="contenu">{{ tweet.contenu }} </div>
      <div class="icons">
        <ul>
          <li class="button"> <icon name="reply"/> </li>
          <a @click="retweet()"> <li class="button"> <icon name="retweet"/> {{ tweet.retweeters.length }} </li> </a>
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
export default {
  name: 'tweet',
  props: ['tweet'],
  components: {Icon},

  methods: {
    moment: function (date) {
      return moment(date)
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
