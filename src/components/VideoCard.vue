<template>
  <!-- padding-left: 10px; padding-right: 10px; -->
  <div style="width: 350px">
    <router-link :to="`/video/${videoInfo.id}`">
      <!-- <v-img
        :src="videoInfo.cover_url"
        outlined
        aspect-ratio="1.77"
        class="white--text align-end"
        >
      </v-img> -->
      <VideoPlayer :options="videoOptions"/>
    </router-link>
    <v-row style="padding-top: 1px; padding-bottom: 12px">
      <v-col cols="10">
        <p style="font-size: 20px; margin-bottom: 0px;color: black;">
          <router-link :to="`/video/${videoInfo.id}`" style="color: black;">
            {{ videoInfo.title }}
          </router-link>
        </p>    
      
        <p style="font-size: 10px; color: #606060;">
          <router-link :to="`/video/${videoInfo.id}`" style="color: black;">
            {{ videoInfo.author_name }}
          </router-link>
          {{ videoInfo.play_cnt }} 观看 <span v-html="`&nbsp;&nbsp;`" />
        </p>
      </v-col>
    </v-row>
  </div>
</template>


<script setup>
import { ref } from 'vue'
import VideoPlayer  from './VideoPlayer.vue'
const props = defineProps({
  video: {
    type: Object,
    default: () => ({})
  }
})

const videoInfo = ref(props.video)

const videoOptions = {
  autoplay: true,
  controls: true,
  sources: [{
    src: require("./abc.mp4"),
    type: 'video/mp4'
  }]
}

</script>