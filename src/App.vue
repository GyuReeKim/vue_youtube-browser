<template>
  <div class="container">
    youtube
    <!-- 3. 사용하기 -->
    <!-- <자식컴포넌트 v-on:자식이올려준함수="부모가사용할함수"/> -->
    <!-- 자식이 올려준 함수, 부모가 사용할 함수의 이름은 서로 달라도 상관 없다. -->
    <SearchBar @inputChange="onInputChange"/>
    <VideoDetail :video="selectedVideo"/>
    <!-- <자식컴포넌트 v-bind:자식한테내려줄이름="부모가가지고있는이름"/> -->
    <!-- 일반적으로 자식한테 내려줄 이름과 부모가 가지고있는 이름은 같게 설정한다. -->
    <!-- 자식에 props를 설정해줘야 한다. -->
    <VideoList :videos="videos" @videoSelect="onVideoSelect"/>
  </div>
</template>

<script>
// 1. 가져오기
import SearchBar from './components/SearchBar'
import VideoList from './components/VideoList'
import VideoDetail from './components/VideoDetail'
import axios from 'axios'

const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY // 이곳에 API 키가 있었다.
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  data: function(){
    // data는 object를 return 해줘야 한다.
    return {
      videos: [],
      // null을 넣으면 기본값이 object이기 때문에 오류가 나지 않는다.
      selectedVideo: null,
    }
  },
  // 2. 등록하기
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  methods: {
    onInputChange(inputValue){
      // console 창에 입력값이 입력된 대로 출력된다.
      // console.log(inputValue)
      // 어디로 요청을 보낼지, 어떤 값을 요청보낼지
      axios.get(API_URL, {
        params: {
          // 기본 설정
          key: API_KEY,
          part: 'snippet',
          type: 'video',
          // 문자열을 가지고 검색해주기
          q: inputValue
        }
      })
      .then((response)=>{
        console.log(response)
        // videos: Array[5]
        // 5개의 Object가 반환되는 이유는 youtube api의 default값이 5개이기 때문이다.
        this.videos = response.data.items
      })
      .catch((error)=>{
        console.log(error)
      })
    },
    onVideoSelect(video){
      console.log(video)
      this.selectedVideo = video

    }
  },
}
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
