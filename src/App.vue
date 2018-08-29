<template>
    <div>
        <SearchBar @termChange="onTermChange"/>
        <VideoList />
    </div>
</template>


<script>
import axios from 'axios'
import SearchBar from "./components/SearchBar";
import VideoList from './components/VideoList'

const API_KEY = 'AIzaSyBYO03XC7O8-N-MaL-vzbUq5V-s-KsP4D4'

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
  },
  data() {
      return {
          videos: []
      }
  },
  methods: {
      onTermChange(searchTerm) {
          axios.get('https://www.googleapis.com/youtube/v3/search', {
              params: {
                  key: API_KEY,
                  type: 'video',
                  part: 'snippet',
                  q: searchTerm
              }
          })
          .then(res => {
              this.videos = res.data.items
          });
      }
  }
};
</script>