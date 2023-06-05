<script setup>
import {ref} from 'vue'

let input = ref ("")
let output = ref ("")

async function search () {
    const response = await fetch ('https://api.dictionaryapi.dev/api/v2/entries/en/' + input.value);
    output = response

}
</script>

<template>
 <nav>
  <router-link to="/">Home</router-link>
  <router-link to="/search">Search</router-link>
  <router-link to="/contact">Contact Us</router-link>
 </nav>

 <br>
 
 <v-text-field label="Search" @keydown.enter="search" v-model="input"></v-text-field>
 <button @click="search">FETCH</button>
 {{ output.value }}
</template>

<style >
</style>
