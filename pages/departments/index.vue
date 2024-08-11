<!-- All categories applications -->
<template>
  <div class="category-page">
    <Head>
      <Title>Інгредієнти</Title>
      <Meta name="og:title" :content="`Інгредієнти`" />
      <Meta name="og:image" :content="images.banner" />
    </Head>
    <div class="container">
      <AppPageBanner title="Інгредієнти" :img="images.banner" />

      <div class="row categories-list gy-5">
        <div class="col-12 col-lg-4">
          <NuxtLink class="category-card__link" to="/pharm">
            <CategoryCard :name="pharmTitle" :image="images.pharm" />
          </NuxtLink>
        </div>
        <div class="col-12 col-lg-4">
          <NuxtLink class="category-card__link" to="/food">
            <CategoryCard :name="foodTitle" :image="images.food" />
          </NuxtLink>
        </div>
        <div class="col-12 col-lg-4">
          <NuxtLink class="category-card__link" to="https://indelcosm.com.ua/">
            <CategoryCard :name="cosmTitle" :image="images.cosm" />
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  async setup() {
    try {
      const { findOne } = useStrapi();
      const media = useStrapiMedia();

      const ingredientsInfo = await findOne("ingredienty-stranicza", {
        populate: {
          food_image: "*",
          pharm_image: "*",
          cosm_image: "*",
          banner: "*",
        },
      });

      const foodTitle = ingredientsInfo.data?.attributes?.food_name;
      const pharmTitle = ingredientsInfo.data?.attributes?.pharm_name;
      const cosmTitle = ingredientsInfo.data?.attributes?.cosm_name;

      const images = {
        banner: `${media}${ingredientsInfo.data?.attributes?.banner?.data?.attributes?.url}`,
        food: `${media}${ingredientsInfo.data?.attributes?.food_image?.data?.attributes?.url}`,
        pharm: `${media}${ingredientsInfo.data?.attributes?.pharm_image?.data?.attributes?.url}`,
        cosm: `${media}${ingredientsInfo.data?.attributes?.cosm_image?.data?.attributes?.url}`,
      };

      return {
        foodTitle,
        pharmTitle,
        cosmTitle,
        images,
      };
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
