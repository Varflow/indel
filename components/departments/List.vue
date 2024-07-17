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
import orderby from "lodash.orderby";

export default {
  async setup() {
    const departments = [
      { name: "Фармацевтика", video: "/videos/pharm.mp4", link: "" },
      { name: "Харчова", video: "/videos/food.mp4", link: "" },
      { name: "Косметика", video: "/videos/cosm.mp4", link: "" },
    ];

    // const media = useStrapiMedia();
    // const { find } = useStrapi();

    // const departments = await find("napravleniyas", {
    //   populate: "*",
    // });

    // console.log(departments);

    // const departmentsForView = departments.data.map((department) => {
    //   return {
    //     ...department.attributes,
    //     image: `${media}${department.attributes.image.data?.attributes.url}`,
    //   };
    // });

    // const orderedDepartments = orderby(departmentsForView, ["order"], ["asc"]);

    // return {
    //   departments: orderedDepartments,
    // };

    return {
      departments,
    };
  },
};
</script>

<style lang="scss" scoped></style>
