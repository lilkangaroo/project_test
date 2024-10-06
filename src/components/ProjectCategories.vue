<template>
  <div class="project_cat">
    <button
      v-for="category in project_categories"
      :key="category.id"
      @click="selectCategory(category.id)"
    >
      {{ category.name }}
    </button>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      project_categories: [],
    };
  },
  methods: {
    selectCategory(categoryID) {
      this.$emit("selectedCategory", categoryID);
    },
    async fetchCategories() {
      try {
        const response = await axios.get(
          "https://api.test.cyberia.studio/api/v1/project-categories"
        );
        this.project_categories = response.data.items;
      } catch (e) {
        alert("Ошибка загрузки категорий проекта");
      }
    },
  },
  mounted() {
    this.fetchCategories();
  },
};
</script>
<style></style>
