<template>
  <!-- <HelloWorld /> -->

  <v-container>
    <v-col v-for="item in videoList">
      <VideoCard :video="item" />
    </v-col>
    <VideoCard :video="video_item"/>
    
  </v-container>

</template>

<script setup>
import HelloWorld from '@/components/HelloWorld.vue'
import VideoCard from '@/components/VideoCard.vue'

const videoList = []

const video_item = {
  id: 1,
  video_url: "",
  cover_url: "https://cdn.vuetifyjs.com/images/parallax/material.jpg",
  play_cnt: 100,
  title: "title_test",
  author_name: "chancy",
  create_time: "10-21"
}

// function getVideoList() {
//   fetch(`/video/feed`, {
//     headers: {
//       'Content-Type': 'application/json; charset=UTF-8',
//     },
//     method: 'GET',
//   }).then(response => response.json())
//     .then(json => {
//       this.videoList = json.data.list
//     })
//     .catch(e => {
//       return null
//     })
// }

</script>
