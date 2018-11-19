<template>
  <div class= "container mx-auto">
    <div>{{ game.name }}</div>
    <!-- <div>{{ game.publishers[0].name }}</div> -->
    <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover">
    <p>{{ game.summary }}</p>
    <div v-for= "platform in game.platforms">{{ platform.name }}</div>
    <div>{{new Date(game.first_release_date).toDateString()}}</div>
    <a :href="getOfficialWebsite">Official Website</a>
    <div>{{ game.summary}}</div>
    <div>{{game.total_rating}}</div>
    <div v-for= "screenshot in game.screenshots"><img :src="screenshot.url.replace('t_thumb', 't_screenshot_med')" alt="screenshot">

    </div>
  </div>
</template>


<script>

import axios from 'axios'

  export default {

  asyncData ({ params, error }) {
    const proxyurl = "https://cors-anywhere.herokuapp.com/"

    return axios.get(`${proxyurl}https://api-endpoint.igdb.com/games/${params.id}/?fields=name,cover,summary,first_release_date,websites,total_rating,screenshots`)
    .then((res) => {
      return {
        game: res.data[0]
      }
    })
    .catch((e) => {
      console.log(e)
      })
  },
  head () {
    return {
      title: this.game.name + ' | Video Games '
    }
  }
}


</script>
