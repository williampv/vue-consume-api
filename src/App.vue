<template>
  <div>
    <div class="hero is-white is-gradient is-bold">

      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">R&M</span>
          <span class="subtitle">Characters</span>
        </h1>

        <button class="button is-success is-rounded" @click="fetch">GET</button>
      </div>

    </div>

    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <div class="column is-12-mobile is-4-desktop is-4-tablet" v-for="character of characters" v-bind:key="character.id">
          <div class="card">
            <div class="card-header"><img v-bind:src="character.image" v-bind:alt="character.name"></div>
            <div class="card-content">
              <h3 class="title is-size-4">{{ character.name }}</h3>
              <button class=" button is-success is-rounded is-small">See more</button>
            </div>
          </div>
        </div>
      </div>
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
