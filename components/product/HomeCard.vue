<template>
  <div class="product-card">
    <NuxtLink :to="link" class="product-card__link">
      <div class="product-card__image-wrapper">
        <img :src="image" :alt="name" class="product-card__image" />
      </div>
    </NuxtLink>
    <h4 class="product-card__category">{{ category }}</h4>
    <NuxtLink :to="link" class="product-card__link">
      <h4 class="product-card__name" v-html="name"></h4>
    </NuxtLink>
    <div class="product-card__actions">
      <AppButton variant="black" @click="openSubmitModal"
        >Замовити взірець</AppButton
      >
    </div>
  </div>
  <ProductSubmitModal :title="name" />
</template>

<script>
import Micromodal from "micromodal";

export default {
  props: ["name", "image", "link"],
  methods: {
    openSubmitModal() {
      Micromodal.show("submit-modal");
    },
  },
};
</script>
