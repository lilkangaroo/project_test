<template>
  <section class="project">
    <h2 class="project__title">{{ project.title }}</h2>
    <img class="project__image" :src="project.image" alt="logo" />
  </section>
</template>

<script>
export default {
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss"></style>
