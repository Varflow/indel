<template>
  <div
    ref="megaMenu"
    class="mega-menu"
    :class="{ 'mega-menu--shown': shown }"
    data-el="menu"
  >
    <div class="arrow"></div>
    <img
      src="/images/logo-icon.svg"
      alt=""
      class="decoration"
      id="bottom-right"
    />
    <!-- <img src="/images/logo-icon.svg" alt="" class="decoration" id="top-right" /> -->
    <div class="container">
      <div class="mega-menu__row">
        <div class="mega-menu__column">
          <div class="mega-menu-sections__list">
            <!-- <div class="mega-menu__title">Інгредієнти</div> -->
            <div class="mega-menu__section-item">
              <NuxtLink to="/pharm"> Фармацевтичні </NuxtLink>

              <div
                class="mega-menu-categories__button"
                @click="selectSection('pharm')"
              >
                <svg
                  width="14"
                  height="14"
                  viewBox="0 0 14 14"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M9.49686 6.69064C9.66771 6.8615 9.66771 7.13851 9.49686 7.30936L5.12186 11.6844C4.95101 11.8552 4.674 11.8552 4.50314 11.6844C4.33229 11.5135 4.33229 11.2365 4.50314 11.0656L8.56878 7L4.50314 2.93436C4.33229 2.7635 4.33229 2.4865 4.50314 2.31564C4.674 2.14479 4.95101 2.14479 5.12186 2.31564L9.49686 6.69064Z"
                    fill="#0F172A"
                  />
                </svg>
              </div>
            </div>
            <div class="mega-menu__section-item">
              <NuxtLink to="/food"> Харчові </NuxtLink>
              <div
                class="mega-menu-categories__button"
                @click.stop="selectSection('food')"
              >
                <svg
                  width="14"
                  height="14"
                  viewBox="0 0 14 14"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M9.49686 6.69064C9.66771 6.8615 9.66771 7.13851 9.49686 7.30936L5.12186 11.6844C4.95101 11.8552 4.674 11.8552 4.50314 11.6844C4.33229 11.5135 4.33229 11.2365 4.50314 11.0656L8.56878 7L4.50314 2.93436C4.33229 2.7635 4.33229 2.4865 4.50314 2.31564C4.674 2.14479 4.95101 2.14479 5.12186 2.31564L9.49686 6.69064Z"
                    fill="#0F172A"
                  />
                </svg>
              </div>
            </div>
            <a
              href="https://indelcosm.com.ua"
              class="mega-menu__section-item"
              target="_blank"
            >
              Косметичні
            </a>
          </div>
        </div>
        <div class="mega-menu__column" v-if="currentSection">
          <div class="mega-menu-categories__list" v-if="currentSection">
            <div
              class="mega-menu-categories__item"
              v-for="category of currentSection"
            >
              <NuxtLink :to="`/${currentSection[0].section}/${category.id}`">
                {{ category.name }}
              </NuxtLink>

              <div
                class="mega-menu-categories__button"
                @click.stop="selectCategory(category.name)"
                v-if="Boolean(category.children?.length)"
              >
                <svg
                  width="14"
                  height="14"
                  viewBox="0 0 14 14"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M9.49686 6.69064C9.66771 6.8615 9.66771 7.13851 9.49686 7.30936L5.12186 11.6844C4.95101 11.8552 4.674 11.8552 4.50314 11.6844C4.33229 11.5135 4.33229 11.2365 4.50314 11.0656L8.56878 7L4.50314 2.93436C4.33229 2.7635 4.33229 2.4865 4.50314 2.31564C4.674 2.14479 4.95101 2.14479 5.12186 2.31564L9.49686 6.69064Z"
                    fill="#0F172A"
                  />
                </svg>
              </div>
            </div>
          </div>
        </div>
        <div class="mega-menu__column" v-if="currentCategory">
          <div class="mega-menu-categories__list" v-if="currentCategory">
            <NuxtLink
              class="mega-menu-categories__item"
              v-for="subcategory of currentCategory.children"
              :to="`/subcategory/${subcategory.id}`"
            >
              {{ subcategory.name }}
            </NuxtLink>
          </div>
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
    return {
      id: collection.id,
      name: collection.attributes.Name,
      section: collection.attributes.section,
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
  props: ["shown"],
  emits: ["close"],
  data() {
    return {
      currentSection: null,
      currentCategory: null,
      pharmForView: [],
      foodsForView: [],
    };
  },

  async mounted() {
    try {
      const { find } = useStrapi();
      const categories = await find("categories", {
        populate: {
          pod_kategoriyas: "*",
        },
      });

      const pharm = categories.data.filter(
        (category) => category.attributes.section === "pharm"
      );
      const foods = categories.data.filter(
        (category) => category.attributes.section === "food"
      );

      const pharmForView = toView(pharm);
      const foodsForView = toView(foods);

      this.pharmForView = pharmForView;
      this.foodsForView = foodsForView;
    } catch (error) {
      console.log(error);
    }
  },

  watch: {
    $route: {
      immediate: true,
      handler() {
        // this.currentSection = null;
        // this.currentCategory = null;
        // this.$emit("close");
      },
    },
    shown: {
      immediate: true,
      handler(_shown) {
        let onCloseTimeout;
        let onOpenTimeout;

        if (!_shown) {
          onCloseTimeout = setTimeout(() => {
            this.currentSection = null;
            this.currentCategory = null;
          }, 150);
        }

        if (_shown) {
          onOpenTimeout = setTimeout(() => {
            document.addEventListener("click", this.watchClickOutside);
          }, 50);
        }

        if (!_shown) {
          document.removeEventListener("click", this.watchClickOutside);
        }

        // clearTimeout(onCloseTimeout);
        // clearTimeout(onOpenTimeout);
      },
    },
  },

  methods: {
    selectSection(section) {
      this.currentCategory = null;
      this.currentSection =
        section === "pharm" ? this.pharmForView : this.foodsForView;
    },
    selectCategory(name) {
      this.currentCategory = this.currentSection.find(
        (category) => category.name === name
      );
    },
    watchClickOutside(event) {
      if (!this.$refs.megaMenu.contains(event.target)) {
        this.$emit("close");
      }
    },
  },
};
</script>
