<template>
  <div class="section-posts">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title" v-if="texts">
          {{ texts.career_section_title }}
        </h2>
      </div>

      <div class="section-text" v-html="texts.career_section_text"></div>

      <div class="section-actions">
        <NuxtLink to="/career" class="link-without-decoration">
          <AppButton variant="black" v-if="texts">{{
            texts.career_section_button_text
          }}</AppButton>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["texts"],
};
</script>
