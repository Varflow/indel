<!-- All categories applications -->
<template>
  <div class="category-page">
    <Head>
      <Title>Фармацевтичні інгредієнти</Title>
      <Meta name="og:title" :content="`Фармацевтичні інгредієнти`" />
      <Meta name="og:image" content="/images/banners/pharm_cover.png" />
    </Head>
    <div class="container">
      <AppPageBanner
        title="Фармацевтичні інгредієнти"
        img="/images/banners/pharm_cover.png"
      />

      <div class="row categories-list gy-5">
        <div class="col-12 col-lg-4" v-for="category of pharmsForView">
          <NuxtLink
            class="category-card__link"
            :to="
              category.children && category.children.length
                ? `/pharm/${category.id}`
                : `/category/${category.id}`
            "
          >
            <CategoryCard
              :name="category.name"
              :image="category.image ? `${media}${category.image}` : null"
            />
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const toView = (collection) => {
  if (!collection) {
    return [];
  }

  return collection.map((collection) => {
    console.log(collection);
    return {
      id: collection.id,
      name: collection.attributes.Name,
      image: collection.attributes.image.data?.attributes.url,
      children: !collection.attributes.pod_kategoriyas?.data.length
        ? null
        : collection.attributes.pod_kategoriyas?.data.map((subcategory) => {
            return {
              id: subcategory.id,
              name: subcategory.attributes.name,
            };
          }),
    };
  });
};

export default {
  async setup() {
    try {
      const { find } = useStrapi();
      const media = useStrapiMedia();

      const categories = await find("categories", { populate: "*" });

      const pharms = categories.data.filter(
        (category) => category.attributes.section === "pharm"
      );

      const pharmsForView = toView(pharms);

      return {
        pharmsForView,
        media,
      };
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
