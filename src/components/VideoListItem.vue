<template>
  <ol>
    <li class="list-group-item media" @click="onVideoSelect">
      <img :src="thumbnailUrl" alt="thumbnail" class="mr-3" />
      <div class="media-body">
        {{ videoTitle }}
      </div>
    </li>
  </ol>
</template>

<script>
export default {
  name: "VideoListItem",
  props: {
    video: Object
  },
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    },
    videoTitle() {
      return this.$sanitize(this.video.snippet.title);
    }
  },
  methods: {
    onVideoSelect() {
      this.$emit("videoSelect", this.video);
    }
  }
};
</script>

<style scoped>
li {
  display: flex;
  flex-flow: row wrap;
  cursor: pointer;
}

li:hover {
  background-color: #eee;
}
</style>
