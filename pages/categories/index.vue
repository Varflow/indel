<!-- All categories applications -->
<template>
  <div class="category-page">
    <Head>
      <Title>{{ sections[section] }}</Title>
      <Meta name="og:title" :content="sections[section]" />
      <Meta name="og:image" content="/images/banners/ingredients.jpeg" />
    </Head>
    <div class="container">
      <AppPageBanner
        :title="sections[section]"
        img="/images/banners/ingredients.jpeg"
      />

      <div class="row categories-list gy-5">
        <div class="col-12 col-lg-4" v-for="category of categoriesForView">
          <NuxtLink
            class="category-card__link"
            :to="
              category.children && category.children.length
                ? `/${section}/${category.id}`
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
      const route = useRoute();

      const sections = {
        pharm: "Фармацевтичні інгредієнти",
        food: "Харчові інгредієнти",
      };
      console.log("route.query.section", route.query.section);
      const categories = await find("categories", { populate: "*" });

      const currentCategories = categories.data.filter(
        (category) => category.attributes.section === route.query.section
      );

      const categoriesForView = toView(currentCategories);

      return {
        categoriesForView,
        media,
        section: route.query.section,
        sections,
      };
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
