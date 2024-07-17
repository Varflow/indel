<template>
  <div class="main-page">
    <div class="main-page__header">
      <NuxtLink to="/main" class="main-page__logo">
        <MainLogo />
      </NuxtLink>
    </div>

    <div class="main-page__departments">
      <div class="container">
        <DepartmentsList />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: "outside",
});
</script>
