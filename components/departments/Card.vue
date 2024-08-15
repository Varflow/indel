<template>
  <a :href="link" target="_blank" class="department-card">
    <div class="department-card__image-wrapper">
      <!-- <img :src="image" :alt="name" /> -->
      <video
        :src="video"
        :class="`${center ? 'center' : ''}`"
        ref="video"
        muted
        autoplay
        loop
        playsinline
      ></video>
      <h4 class="department-card__title">{{ name }}</h4>
      <NuxtLink class="department-card__button">
        <span>Детальніше</span>
      </NuxtLink>
    </div>
  </a>
</template>

<script>
export default {
  props: ["name", "video", "link", "center"],

  mounted() {
    this.$refs.video.play();
  },
};
</script>
