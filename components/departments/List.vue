<template>
  <div class="departments-list">
    <DepartmentsCard
      v-for="department in departments"
      :name="department.name"
      :image="department.image"
      :link="department.link"
    />
  </div>
</template>

<script>
import orderby from "lodash.orderby";

export default {
  async setup() {
    const media = useStrapiMedia();
    const { find } = useStrapi();

    const departments = await find("napravleniyas", {
      populate: "*",
    });

    console.log(departments);

    const departmentsForView = departments.data.map((department) => {
      return {
        ...department.attributes,
        image: `${media}${department.attributes.image.data?.attributes.url}`,
      };
    });

    const orderedDepartments = orderby(departmentsForView, ["order"], ["asc"]);

    return {
      departments: orderedDepartments,
    };
  },
};
</script>

<style lang="scss" scoped></style>
