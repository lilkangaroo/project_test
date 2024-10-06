<template>
  <section>
    <h1>Кейсы</h1>
    <ProjectCategories @selectedCategory="selectCategory" />
    <TheProject
      class="project"
      v-for="project in filterProjects"
      :key="project.id"
      :project="project"
    />
  </section>
</template>

<script>
import TheProject from "./TheProject.vue";
import ProjectCategories from "./ProjectCategories.vue";

export default {
  components: { TheProject, ProjectCategories },
  props: {
    projects: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedCategoryID: null,
    };
  },
  methods: {
    selectCategory(categoryID) {
      this.selectedCategoryID = categoryID;
    },
  },
  computed: {
    filterProjects() {
      if (this.selectedCategoryID == null) {
        return this.projects;
      } else {
        return this.projects.filter((project) =>
          project.categories.some(
            (category) => category.id === this.selectedCategoryID
          )
        );
      }
    },
  },
};
</script>

<style></style>
