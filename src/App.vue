<template>
  <div id="app" class="container">
    <SearchBar @termChange="onTermChange" />
    <VideoDetail :video="selectedVideo" />
    <VideoList @videoSelect="onVideoSelect" :videos="videos" />
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

const API_KEY = "AIzaSyDxkKpJhXkyexojzfaVwM5FwagpxPT0wq8";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      videos: [],
      selectedVideo: null
    };
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm
          }
        })
        .then(response => (this.videos = response.data.items));
    }
  }
};
</script>

<style></style>
