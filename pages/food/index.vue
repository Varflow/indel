<!-- All categories applications -->
<template>
  <div class="category-page">
    <Head>
      <Title>Харчові інгредієнти</Title>
      <Meta name="og:title" :content="`Харчові інгредієнти`" />
      <Meta name="og:image" content="/images/banners/food_cover.jpg" />
    </Head>
    <div class="container">
      <AppPageBanner
        title="Харчові інгредієнти"
        img="/images/banners/food_cover.jpg"
      />

      <div class="row categories-list gy-5">
        <div class="col-12 col-lg-4" v-for="category of foodForView">
          <NuxtLink
            class="category-card__link"
            :to="
              category.children && category.children.length
                ? `/food/${category.id}`
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
import orderby from "lodash.orderby";
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
      order: collection.attributes.order,
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

      const foodCategories = categories.data.filter(
        (category) => category.attributes.section === "food"
      );

      const foodForView = orderby(toView(foodCategories), ["order"], ["asc"]);

      return {
        foodForView,
        media,
      };
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
