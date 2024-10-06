<template>
  <div class="categories">
    <button
      class="categories__category"
      :class="{ selected: category.id === selectedCategory }"
      v-for="category in project_categories"
      :key="category.id"
      @click="selectCategory(category.id)"
    >
      {{ category.name }}
    </button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      project_categories: [],
      selectedCategory: null,
    };
  },
  methods: {
    selectCategory(categoryID) {
      this.selectedCategory = categoryID;
      this.$emit('selectedCategory', categoryID);
    },
    async fetchCategories() {
      try {
        const response = await axios.get(
          'https://api.test.cyberia.studio/api/v1/project-categories',
        );
        this.project_categories = response.data.items;
      } catch {
        alert('Ошибка загрузки категорий проекта');
      }
    },
  },
  mounted() {
    this.fetchCategories();
  },
};
</script>
<style lang="scss">
.categories {
  display: flex;
  align-items: center;
  justify-content: space-between;

  &__category {
    background-color: $backgroud-button;
    color: $color-text;
    border: none;
    padding: 10px 25px;
    border-radius: 7px;
    font-family: $base-font;
    font-size: $button-size;
    transition: background-color 0.5s;

    &.selected {
      background-color: $background-button-hover;
    }

    &:hover {
      background-color: $background-button-hover;
    }
  }
}
</style>
