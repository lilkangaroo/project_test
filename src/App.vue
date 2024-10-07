<template>
  <div class="app">
    <TheHeader />
    <div class="container">
      <TheBreadcrumbs />
      <ProjectList :projects="projects" />
      <FeedbackForm />
    </div>
    <TheFooter />
  </div>
</template>

<script>
import axios from 'axios';

import TheHeader from '@/components/TheHeader.vue';
import TheBreadcrumbs from '@/components/TheBreadcrumbs.vue';
import ProjectList from './components/ProjectList.vue';
import FeedbackForm from '@/components/FeedbackForm.vue';
import TheFooter from '@/components/TheFooter.vue';

export default {
  components: {
    TheHeader,
    TheBreadcrumbs,
    ProjectList,
    FeedbackForm,
    TheFooter,
  },
  data() {
    return {
      projects: [],
    };
  },
  methods: {
    async fetchProjects() {
      try {
        const response = await axios.get(
          'https://api.test.cyberia.studio/api/v1/projects',
        );
        this.projects = response.data.items;
      } catch {
        alert('Ошибка загрузки проектов');
      }
    },
  },
  mounted() {
    this.fetchProjects();
  },
};
</script>

<style lang="scss">
.container {
  margin: 0px 200px 0;
  flex-grow: 1;
  flex-shrink: 0;
}
</style>
