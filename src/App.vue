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
      <div 
        class="columns is-desktop is-mobile is-tablet is-multiline is-centered"
      >
        <character 
          v-for="character of characters" 
          v-bind:key="character.id" 
          v-bind:character = "character">
        </character>
      </div>

      <nav class="pagination is-centered" role="navegation" aria-label="pagination">
        <a class="pagination-previous" v-on:click="changePage( page - 1 )">Previous</a>

        <ul class="pagination-list">
          <li>
            <a class="pagination-link is-current">{{ page }}</a>
          </li>
        </ul>

        <a class="pagination-next" v-on:click="changePage( page + 1 )">Next</a>
      </nav>
    </div>

  </div>
</template>

<script>
// libraries
import axios from "axios";
import Character from './components/Character.vue'

export default {
  components: {
    Character
  },
  data: function() {
    return {
      characters: [],
      page: 1,
      pages: 1
    }
  },
  created() {
    this.fetch()
  },
  methods: {
    fetch(){
      const params = {
        page: this.page
      }      

      let result = axios
        .get("https://rickandmortyapi.com/api/character/", { params })
        .then(res => {
          this.characters = res.data.results
          this.pages = res.data.info.pages
          console.log(res.data)
        })
        .catch(err => {
          console.log(err)
        }) 
      
    },
    changePage(page) {
      this.page = page <= 0 || page > this.pages ? this.page : page
      this.fetch()
    }
  }
}
</script>

<style scoped>
</style>
