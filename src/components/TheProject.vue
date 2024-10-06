<template>
  <section>
    <div class="project">
      <h2>{{ project.title }}</h2>
      <img :src="project.image" alt="logo" />
    </div>
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
