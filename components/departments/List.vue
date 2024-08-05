<template>
  <div class="departments-list">
    <DepartmentsCard
      v-for="department in departments"
      :name="department.name"
      :video="department.video"
      :link="department.link"
      :center="department.center"
    />
  </div>
</template>

<script>
export default {
  props: ["departments"],
};
</script>

<style lang="scss" scoped></style>
