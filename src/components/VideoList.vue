<template>
  <ul class="list-group">
    <!-- video.etag는 id 대신 사용 -->
    <!-- <@자식이올린함수="부모에서실행할함수>" -->
    <VideoListItem v-for="video in videos" :key="video.etag" :video="video" @videoSelect="onVideoSelect"/>
    <!-- input에 말도 안되는 값을 입력하면 videos.length에 0이 출력된다. -->
    <!-- {{videos.length}} -->
  </ul>
</template>

<script>
import VideoListItem from './VideoListItem'

export default {
  name: 'VideoList',
  props: {
    videos: Array,
  },
  components: {
    VideoListItem,
  },
  methods: {
    onVideoSelect(video){
      this.$emit('videoSelect', video)
    }
  }
}
</script>

<style>

</style>