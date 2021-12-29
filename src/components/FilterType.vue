<template>
  <div class="filter-type">
    <p>{{ filter.name }}</p>
    <video controls autoplay :class="filter.name" @click="selectFilter">
      <source :src="getVideoUrl(postVideo)" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
  </div>
</template>

<script>
import EventBus from "../event-bus.js";

export default {
  name: "FilterType",
  props: {
    filter: Object,
    image: String,
  },
  methods: {
    selectFilter() {
      EventBus.$emit("filter-selected", { filter: this.filter.name });
    },
    getVideoUrl(name) {
      var images = require.context("../assets/", false, /\.mp4$/);
      return images("./" + name + ".mp4");
    },
  },
};
</script>

<style lang="scss" src="../styles/filter-type.scss"></style>
