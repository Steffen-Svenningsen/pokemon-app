<script setup>
import axios from "axios"
import { ref } from "vue"

const pokemonName = ref("Ditto")
const pokemonImage = ref("https://img.pokemondb.net/sprites/home/normal/2x/ditto.jpg")

const getNewPokemon = () => {
  axios.get('https://pokeapi.co/api/v2/pokemon?limit=493')
    .then(response => {
      pokemonName.value = response.data.results[Math.floor(Math.random() * (492 - 0) + 0)].name;
      pokemonImage.value = "https://img.pokemondb.net/sprites/home/normal/2x/".concat(pokemonName.value, ".jpg")
    })
}
</script>

<template>
    <div class="pokemon-page">
        <h1 class="title">Pokédex</h1>
        <h3>Gen I - Gen IV</h3>
        <div class="pokemon-card">
          <h1 class="name">{{ pokemonName }}</h1>
          <img v-bind:src="pokemonImage" width="200" height="200" alt="">
        </div>
        <button @click="getNewPokemon">I choose You!</button>
    </div>
</template>

<style lang="sass" scoped>
.pokemon-page
  width: 100%
  height: 100vh
  display: flex
  flex-direction: column
  justify-content: flex-start
  align-items: center
  font-family: "Helvetica", sans-serif
  text-align: center
  background-image: url('../../public/background.webp')
  background-size: cover
  background-position: center top

  .title
    font-size: 2rem
    font-weight: bold
    margin: 4rem 0 0 0
    color: white
    -webkit-text-stroke: 1px black

  h3
    margin: 0.65rem 0 1.5rem 0

  .pokemon-card
    width: fit-content
    height: fit-content
    padding: 3rem
    margin: 1rem
    border-radius: 50px
    background: #ffffff
    box-shadow:  20px 20px 60px rgba(0, 0, 0, 0.50), -20px -20px 60px rgba(0, 0, 0, 0.50)
    position: fixed
    top: 22.5%

    h1
      text-transform: capitalize
      font-size: 1.25rem
      font-weight: bold
      margin-bottom: 0.5rem

    img
      width: 100%
      height: auto

  button
    padding: 0.75rem 0.75rem 0.75rem 2.5rem
    outline: none
    border: none
    cursor: pointer
    border-radius: 4px
    box-shadow: 4px 4px 4px rgba(0, 0, 0, 0.50)
    background-color: white
    font-size: 1.5rem
    font-weight: bold
    border: 2px solid black
    margin-top: 1.75rem
    position: fixed
    bottom: 2rem

    &::before
      content: url(../../public/favicon.ico)
      position: absolute
      z-index: -1
      top: -10px
      left: -12px

    &:active
      transform: translateY(3px)
      box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.35)

@media (max-width: 460px)
  .pokemon-page
    background-position: left top
</style>