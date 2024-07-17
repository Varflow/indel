<template>
  <a :href="link" target="_blank" class="department-card">
    <div class="department-card__image-wrapper">
      <!-- <img :src="image" :alt="name" /> -->
      <video :src="video" autoplay muted loop></video>
      <h4 class="department-card__title">{{ name }}</h4>
      <NuxtLink class="department-card__button">
        <span> Переглянути товари </span>
      </NuxtLink>
    </div>
  </a>
</template>

<script>
export default {
  props: ["name", "video", "link"],
};
</script>
