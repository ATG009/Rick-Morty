<template>
    <div class="character-card">
      <img :src="character.image" alt="Character Image">
      <h2>{{ character.name }}</h2>
      <p>Status: {{ character.status }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CharacterCard',
    props: {
      character: Object
    }
  }
  </script>
  
  <style>
  .character-card {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px;
    text-align: center;
  }
  </style>
  