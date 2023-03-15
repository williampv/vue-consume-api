<template>
  <div>
    <h1 class="title">Vue API</h1>
    <button @click="fetch">GET</button>

    <div v-for="character of characters" v-bind:key="character.id">
      {{ character.name }}
    </div>
  </div>
</template>

<script>
// libraries
import axios from "axios";

export default {
  data: function() {
    return {
      characters: []
    }
  },

  methods: {
    fetch(){
      let result = axios
        .get("https://rickandmortyapi.com/api/character")
        .then(res => {
          this.characters = res.data.results
          console.log(res.data)
        })
        .catch(err => {
          console.log(err)
        }) 
      
    }
  }
}
</script>

<style scoped>
</style>
