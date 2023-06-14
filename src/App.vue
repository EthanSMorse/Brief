<script setup>
import {ref} from 'vue'

let input = ref ("")
let output = ref ("")
let blank = ref (false)

async function search () {
    const response = await fetch ('https://api.dictionaryapi.dev/api/v2/entries/en/' + input.value);
    output.value = await response.json()
    console.log (response)
    blank.value = true
}
</script>

<template>
  <v-app id="inspire">
    <v-app-bar flat id="header">
      <v-container class="fill-height d-flex align-center">
        <img id="profile" src="ScreenShot2023-06-05at2.11.44PM.png">
        <h1 id="header-h1">Words 4 Idiots</h1>
      </v-container>
    </v-app-bar>

    <v-main id="main">
      <v-container>
        <v-row>

          <v-col>
            <v-sheet
              min-height="70vh"
              rounded="lg"
              id="search"
            >
                <v-text-field label="Search" @keydown.enter="search" v-model="input"></v-text-field>
                <div id="main-text" v-if="blank == true">
                    <h1>Definitions:</h1>
                    <br>
                    <div v-for="definition in output?.[0]?.meanings?.[0]?.definitions">
                        {{ definition.definition }}
                    </div>
                    <br>
                    <h1>Synonyms:</h1>
                    <br>
                      <div v-for="synonym in output?.[0]?.meanings?.[0]?.definitions">
                        <div v-for="value in synonym.synonyms">>
                          {{ value }}
                          <br>
                        </div>
                      </div>
                      <br>
                      <h1>Antonyms:</h1>
                      <br>
                      <div v-for="antonym in output?.[0]?.meanings?.[0]?.definitions">
                        <div v-for="value in antonym.antonyms">
                          {{ value }}
                        </div>
                      </div>
                    <br>
                </div>
                <div v-else>
                  <h1 id="init-text">Type a word into the search bar, press enter, and you'll have all the information you need!</h1>
                </div>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>


<style>
#main-text {
    margin-left: 30px;
}

#init-text {
  text-align: center;
  margin: 30px;
  margin-top: 130px;
}

#header {
  background-color:maroon;
  color: goldenrod;
}

#header-h1 {
  margin-left: 20px;
}

#main {
   background-color: rgb(168, 0, 34);
}

#search {
  background-color: maroon;
  color: goldenrod;
}

#button {
  background-color: maroon;
  color:goldenrod;
}

#profile {
  width: 40px;
  height: 40px;
  border: 1px;
  border-radius: 100%;
}
</style>