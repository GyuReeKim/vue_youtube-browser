<template>
  <!-- li tag를 클릭하면 detail페이지로 넘어가도록 한다. -->
  <li @click="onVideoSelect" class="list-group-item">
    <!-- 직접 Console이나 Vue에서 찾아보자 -->
    <!-- <img :src="video.snippet.thumbnails.default.url" alt=""> -->
    <img :src="thumbnailUrl" class="mr-3">
    {{video.snippet.title}}
  </li>
</template>

<script>
export default {
  name: 'videoListItem',
  props: {
    video: Object,
  },
  computed: {
    thumbnailUrl: function(){
      // 긴 문장들은 computed로 빼는 것이 좋다.
      return this.video.snippet.thumbnails.default.url
    }
  },
  methods: {
    onVideoSelect(){
      this.$emit('videoSelect', this.video)
    }
  }
}
</script>

<style>

</style>