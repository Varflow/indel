<template>
  <div class="main-page">
    <div class="main-page__header">
      <NuxtLink to="/main" class="main-page__logo">
        <MainLogo />
      </NuxtLink>
    </div>

    <div class="main-page__departments">
      <div class="container">
        <DepartmentsList :departments="departments" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: "outside",
});

const departments = [
  { name: "Фармацевтика", video: "/videos/pharm.mov", link: "", center: false },
  { name: "Харчова", video: "/videos/food.mp4", link: "", center: false },
  { name: "Косметика", video: "/videos/cosm.mp4", link: "", center: true },
];
</script>
