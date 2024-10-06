<template>
  <section class="">
    <h1>Кейсы</h1>
    <ProjectCategories @selectedCategory="selectCategory" />
    <div class="projects">
      <TheProject
        class="projects__item"
        v-for="project in filterProjects"
        :key="project.id"
        :project="project"
      />
    </div>
  </section>
</template>

<script>
import TheProject from './TheProject.vue';
import ProjectCategories from './ProjectCategories.vue';

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
            (category) => category.id === this.selectedCategoryID,
          ),
        );
      }
    },
  },
};
</script>

<style lang="scss">
.projects {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 5px;
  padding: 50px 0 0 0;
}
</style>
