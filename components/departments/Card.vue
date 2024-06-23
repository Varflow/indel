<template>
  <a :href="link" target="_blank" class="department-card">
    <div class="department-card__image-wrapper">
      <img :src="image" :alt="name" />
      <h4 class="department-card__title">{{ name }}</h4>
    </div>
  </a>
</template>

<script>
export default {
  props: ["name", "image", "link"],
};
</script>
