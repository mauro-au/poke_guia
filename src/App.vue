<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo_pokemon.png">
    <h1>Poke Guia</h1>
    <label>Nombre</label>
    <input type="text" v-model="pokemon.name">
    <button @click="search">Buscar</button>
    <br>
    <div class="img">
      <img :src="pokePicture">
    </div>
    <h2>Movimientos</h2>
      <li v-for="move in pokeMoves" :key= move>{{move.move.name}}</li>

    <h2>Habilidades</h2>
      <li v-for="abilitie in pokeAbilities" :key= abilitie>{{abilitie.ability.name}}</li>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemon: {
        name: 'pikachu',
        moves: [],
        abilities: []
      }
    }
  },
  methods: {
    search(){
      let name = this.pokemon.name.toLowerCase()
      fetch(`http://pokeapi.co/api/v2/pokemon/${name}`)
        .then(response => response.json())
        .then(response => this.pokemon = response)
    }
  },
  created() {
    this.search()
  },
  computed: {
    pokePicture() {
      return this.pokemon.sprites.front_default
    },
    pokeMoves(){
      return this.pokemon.moves
    },
    pokeAbilities(){
      return this.pokemon.abilities
    }
  }
};


</script>

<style>
  #app{
    text-align: center;
  }
  img{
    margin: 0 auto;
    width: 50vh;
  }
</style>