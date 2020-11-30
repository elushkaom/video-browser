<template>
  <ol>
    <li class="list-group-item media" @click="onVideoSelect">
      <img :src="thumbnailUrl" alt="thumbnail" class="mr-3" />
      <div class="media-body">
        {{ video.snippet.title }}
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
    }
  },
  methods: {
    onVideoSelect() {
      console.log(this.video);
      this.$emit("videoSelect", this.video);
    }
  }
};
</script>

<style scoped>
li {
  display: flex;
  cursor: pointer;
}

li:hover {
  background-color: #eee;
}
</style>
