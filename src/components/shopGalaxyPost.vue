<template>
  <div class="vuegram-post">
    <div class="header level">
      <div class="level-left">
        <img :src="getImgUrl(post.userImage)" v-bind:alt="pic" />
        <span class="username">{{ post.username }}</span>
      </div>
    </div>
    <div class="image-container" @dblclick="like">
      <video controls autoplay>
        <source
          :src="getVideoUrl(post.postVideo)"
          type="video/mp4"
        />
        Your browser does not support the video tag.
      </video>
    </div>
    <div class="content">
      <div class="heart">
        
        <img src="../assets/heart2.png" width="22px" :class="{ fas: this.post.hasBeenLiked }"
          @click="like" alt="logo" />
      </div>
      <p class="likes">{{ post.likes }} likes</p>
      <p class="caption">
        <span>{{ post.username }}</span> {{ post.caption }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "VuegramPost",
  props: {
    post: Object,
  },
  methods: {
    like() {
      this.post.hasBeenLiked ? this.post.likes-- : this.post.likes++;
      this.post.hasBeenLiked = !this.post.hasBeenLiked;
    },
    getImgUrl(name) {
      var images = require.context("../assets/", false, /\.png$/);
      return images("./" + name + ".png");
    },
    getVideoUrl(name) {
      var images = require.context("../assets/", false, /\.mp4$/);
      return images("./" + name + ".mp4");
    },
  },
};
</script>

<style lang="scss" src="../styles/galaxy-post.scss">
</style>
