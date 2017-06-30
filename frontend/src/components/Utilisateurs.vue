<template>
  <div class="utilisateur">
    <label for="utilisateur">Utilisateurs</label> :
      <select @change="onChange($event.target.value)">
         <option disabled value="">Choisissez un utilisateur ...</option>
         <option v-for="utilisateur in utilisateurs" :value="utilisateur.handle">
           {{ utilisateur.prenom }} {{ utilisateur.nom }}
         </option>
      </select>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'utilisateur',
  props: ['utilisateurs'],
  data () {
    return {
      utilisateurs: []
    }
  },

  methods: {
    onChange: function (handle) {
      this.$emit('userChanged', handle)
    }
  }
}
</script>
