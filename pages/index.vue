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
  { name: "Фармацевтика", video: "/videos/1/pharm.mp4", link: "" },
  { name: "Харчова", video: "/videos/1/food.mp4", link: "" },
  { name: "Косметика", video: "/videos/1/cosm.mp4", link: "" },
];
</script>
