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

const route = useRoute();

const departments = [
  {
    name: "Фармацевтика",
    video: `/videos/2/pharm.mp4`,
    link: "",
  },
  { name: "Харчова", video: `/videos/2/food.mp4`, link: "" },
  { name: "Косметика", video: `/videos/${route.params.id}/cosm.mp4`, link: "" },
];
</script>
