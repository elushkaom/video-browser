<template>
  <div id="app" class="container">
    <SearchBar @termChange="onTermChange" />
    <div class="row">
      <VideoList @videoSelect="onVideoSelect" :videos="videos" />
      <VideoDetail :video="selectedVideo" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

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
  computed: {
    getApiKey() {
      return process.env.VUE_APP_API_KEY;
    }
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: this.getApiKey,
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
