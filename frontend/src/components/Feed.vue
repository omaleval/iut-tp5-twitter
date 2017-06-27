<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <ul>
      <li v-for="tweet in tweets" >
        <tweet :tweet="tweet"></tweet>
      </li>
    </ul>

  </div>
</template>




<script>
import Tweet from './Tweet'
export default {
  name: 'feed',
  components: {Tweet},
  props: ['tweets', 'loading']
}
</script>
