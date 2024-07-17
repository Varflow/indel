<template>
  <div class="departments-list">
    <DepartmentsCard
      name="Фармацевтика"
      video="/videos/pharm.mp4"
      link="/pharm"
    />
    <DepartmentsCard name="Харчова" video="/videos/food.mp4" link="/food" />
    <DepartmentsCard
      name="Косметика"
      video="/videos/cosm.mp4"
      link="https://indelcosm.com.ua/"
    />
  </div>
</template>

<script>
export default {
  async setup() {
    const departments = [
      { name: "Фармацевтика", video: "/videos/pharm.mp4", link: "" },
      { name: "Харчова", video: "/videos/food.mp4", link: "" },
      { name: "Косметика", video: "/videos/cosm.mp4", link: "" },
    ];

    return {
      departments,
    };
  },
};
</script>

<style lang="scss" scoped></style>
