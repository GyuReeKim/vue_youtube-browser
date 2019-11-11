<template>
  <!-- video 값이 없으면 null값이 들어와 html에서 주석처리가 되는 것을 확인할 수 있다. -->
  <div v-if="video">
    <!-- detail -->
    <!-- {{video}} -->
    <div>
      <!-- src에 video가 가지고있는 id값으로 embed를 시킨다. -->
      <iframe :src="videoURL" frameborder="0"></iframe>
      <h4>{{video.snippet.title}}</h4>
      <p>{{video.snippet.description}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    video: Object,
  },
  computed: {
    videoURL: function(){
      const videoID = this.video.id.videoId
      return `https://www.youtube.com/embed/${videoID}`
    }
  }
}
</script>

<style>

</style>