<template>
    <div>
      <div>
        <input v-model="name" placeholder="Name">
        <select v-model="status">
          <option value="">All</option>
          <option value="alive">Alive</option>
          <option value="dead">Dead</option>
          <option value="unknown">Unknown</option>
        </select>
        <button @click="applyFilters">Применить</button>
      </div>
      <div class="character-list">
        <CharacterCard v-for="character in characters" :key="character.id" :character="character" />
      </div>
      <div>
        <button @click="prevPage" :disabled="page === 1">Previous</button>
        <button @click="nextPage" :disabled="!info.next">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  import CharacterCard from './CharacterCard.vue'
  
  export default {
    name: 'CharacterList',
    components: {
      CharacterCard
    },
    data() {
      return {
        characters: [],
        info: {},
        page: 1,
        name: '',
        status: ''
      }
    },
    methods: {
      fetchCharacters() {
        axios.get(`https://rickandmortyapi.com/api/character`, {
          params: {
            page: this.page,
            name: this.name,
            status: this.status
          }
        }).then(response => {
          this.characters = response.data.results
          this.info = response.data.info
        })
      },
      applyFilters() {
        this.page = 1
        this.fetchCharacters()
      },
      nextPage() {
        if (this.info.next) {
          this.page++
          this.fetchCharacters()
        }
      },
      prevPage() {
        if (this.page > 1) {
          this.page--
          this.fetchCharacters()
        }
      }
    },
    mounted() {
      this.fetchCharacters()
    }
  }
  </script>
  
  <style>
  .character-list {
    display: flex;
    flex-wrap: wrap;
  }
  </style>
  