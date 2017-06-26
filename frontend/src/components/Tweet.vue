<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
      <div> {{ tweet.auteur }} : {{ tweet.contenu }} </div>
  </div>
</template>




<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>
