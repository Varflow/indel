<template>
  <div class="container">
    <div class="about-banner row g-0">
      <div class="col-lg-6">
        <img :src="banner" alt="" class="about-banner__image" />
      </div>
      <div class="col-lg-6 about-banner__content">
        <div
          v-if="texts"
          class="about-banner__subtitle"
          v-html="texts.first_section_subtitle"
        ></div>
        <!-- <h2 class="about-banner__title" v-if="texts">
          {{ texts.first_section_title }}
        </h2> -->
        <div class="about-banner__actions">
          <NuxtLink to="/company" class="link-without-decoration">
            <AppButton variant="black" v-if="texts">{{
              texts.first_section_button_text
            }}</AppButton>
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["texts"],

  async setup() {
    const media = useStrapiMedia();
    const { findOne } = useStrapi();

    const homeImages = await findOne("glavnaya-kartinki", { populate: "*" });

    console.log("homeImages", homeImages);

    return {
      banner: `${media}${homeImages.data?.attributes?.about_image?.data?.attributes?.url}`,
    };
  },
};
</script>
