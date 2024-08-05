<template>
  <a :href="link" target="_blank" class="department-card">
    <div class="department-card__image-wrapper">
      <!-- <img :src="image" :alt="name" /> -->
      <video
        ref="video"
        :src="video"
        muted
        autoplay
        loop
        :class="`${center ? 'center' : ''}`"
      ></video>
      <h4 class="department-card__title">{{ name }}</h4>
      <NuxtLink class="department-card__button">
        <span> Переглянути товари </span>
      </NuxtLink>
    </div>
  </a>
</template>

<script>
export default {
  props: ["name", "video", "link", "center"],

  // mounted() {
  //   const video = this.$refs.video;
  //   let reverse = false;

  //   // Event listener for when the video ends
  //   video.addEventListener("ended", function () {
  //     reverse = !reverse;
  //     if (reverse) {
  //       playReverse();
  //     } else {
  //       video.currentTime = 0;
  //       video.play();
  //     }
  //   });

  //   // Function to play the video in reverse
  //   function playReverse() {
  //     let fps = 30; // Frames per second
  //     let interval = 1000 / fps;

  //     // Pause the video
  //     video.pause();

  //     // Set interval to go backwards frame by frame
  //     let reverseInterval = setInterval(function () {
  //       video.currentTime -= 1 / fps;
  //       if (video.currentTime <= 0) {
  //         clearInterval(reverseInterval);
  //         reverse = false;
  //         video.currentTime = 0;
  //         video.play();
  //       }
  //     }, interval);
  //   }

  //   // Start playing the video
  //   video.play();
  // },
};
</script>
