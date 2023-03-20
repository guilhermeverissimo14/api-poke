<script setup>
import { onMounted, reactive, ref, computed } from 'vue';

import List from './list.vue'

let url = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")
let pokemons = reactive(ref());
let searchPokemon = ref("")

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
    .then(res => res.json())
    .then(res => {
      pokemons.value = res.results
    });
})

const pokemonsFilter = computed(()=>{
  if(pokemons.value && searchPokemon.value){
    return pokemons.value.filter(pokemons=> pokemons.name.toLowerCase().includes(searchPokemon.value.toLocaleLowerCase()));
  }
  return pokemons.value;

})

</script>

<template>
  <div class="col-sm-12 col-md-6">
    <div class="card">
      <div class="card-body row">

        <div class="mb-3">
          <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Pesquisar" v-model="searchPokemon">
        </div>

        <List v-for="pokemon in pokemonsFilter" :key="pokemon.name" :name="pokemon.name"
          :url="url + pokemon.url.split('/')[6] + '.svg'" />

      </div>
    </div>
  </div>
</template>

<style scoped></style>
