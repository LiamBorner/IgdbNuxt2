<template>
<div class="container mx-auto">
<div class="game-container">
  <nuxt-link :to="'/games/' + game.id" v-for="game in games" :key="game.id" class="block mb-8">

    <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover">
    <div>{{ game.name}}</div>
    <!-- <div>{{ game.genres[0].name}}</div> -->
  </nuxt-link>

    </div>
  </div>

</div>
</div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import axios from 'axios'

export default {
  components: {
    Logo
  },
  asyncData ({ params, error }) {
    const proxyurl = 'https://cors-anywhere.herokuapp.com/'
    return axios.get(`${proxyurl}https://api-endpoint.igdb.com/games/?fields=name,cover,total_rating&filter[rating][gte]=90&order=release_dates.date:desc:min&limit=20`)
    .then((res) => {
      return {
        games: res.data
      }
    })
    .catch((e) => {
      console.log(e)
      })
  },
  data() {
    return {

      }
    }
  }
</script>

<style>

</style>
