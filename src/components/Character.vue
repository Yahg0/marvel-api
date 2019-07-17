<template>
  <div>
    <h1>character export with sucess</h1>
    <p>{{this.$route.params.id}}</p>

    <ul>
        <li v-for="char in character" v-bind:key="char.name">
            {{char.name}}
            {{char.description}}
        </li>
    </ul>
    <img :src="url" alt="">
  </div>
</template>


<script>
/* eslint-disable */
import { public_key } from "../marvel"; /* eslint-disable */
import axios from "axios";
export default {
  name: "Character",

  data() {
      return {
          character: [],
          url: '',
          size: 'standard_large.jpg',
      }
  },

  mounted() {
    this.getCharacter();
  },

  methods: {
    getCharacter: function() {
      var characterId = this.$route.params.id;

      axios
        .get(
          `http://gateway.marvel.com/v1/public/characters/${characterId}?apikey=${public_key}`
        )
        .then(result => {
          console.log(result);

          result.data.data.results.forEach(item => {
              this.character.push(item)

              this.url = `${item.thumbnail.path}/${this.size}`
              console.log(this.url)
          });
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
};
</script>

<style lang="css">
</style>