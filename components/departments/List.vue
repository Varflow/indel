<template>
  <div class="departments-list">
    <DepartmentsCard
      v-for="department in departments"
      :name="department.name"
      :video="department.video"
      :link="department.link"
    />
  </div>
</template>

<script>
export default {
  props: ["departments"],
  // async setup() {
  //   const departments = [
  //     { name: "Фармацевтика", video: "/videos/pharm.mp4", link: "" },
  //     { name: "Харчова", video: "/videos/food.mp4", link: "" },
  //     { name: "Косметика", video: "/videos/cosm.mp4", link: "" },
  //   ];

  //   return {
  //     departments,
  //   };
  // },
};
</script>

<style lang="scss" scoped></style>
