<template>
  <div class="top">
    <h1 class="title">Marvel heroes</h1>
    <h2 class="subtitle">Pesquise por heróis e vilões MCU !</h2>
    <input type="text" name="searchbar" class="searchbar" />
    <br />
    <input type="submit" value="Pesquisar" name="enviar" id="enviar" />

    <div class="heroes-list">
        <ul>
            <li v-for="character in characters" v-bind:key="character.name">
                <router-link :to="{name: 'character', params:{id: character.id} }">{{character.name}}</router-link>
            </li>
        </ul>
    </div>
  </div>
</template>

<script>/* eslint-disable */
import { public_key, secret_key } from '../marvel';
import axios from 'axios'
export default {
  name: "Characters",

  data() {
      return {
          characters: []
      }
  },

  mounted () {
      this.getCharacters();
  },

  methods: {
    getCharacters: function() {
      axios.get(`http://gateway.marvel.com/v1/public/characters?apikey=${public_key}`)
        .then((result) => {
            //console.log(result)

            result.data.data.results.forEach(item => {
                //console.log(item)

                this.characters.push(item)
            });

        })/* eslint-disable */
      .catch((error) =>{

          //console.log(error)

      });
    }
  }

};
</script>

<style lang="css">
.top {
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  display: block;
}
</style>