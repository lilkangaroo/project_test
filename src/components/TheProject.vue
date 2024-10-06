<template>
  <section class="project">
    <div
      class="project__background-img"
      :style="{ backgroundImage: `url(${project.image})` }"
    >
      <h2 class="project__project-title">{{ project.title }}</h2>
      <img class="project__image-corner" src="../img/corner.png" />
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

<style lang="scss" scoped>
.project {
  &__background-img {
    width: 387px;
    height: 378px;
    margin-bottom: 40px;
    position: relative;
    background-size: cover;
    background-position: center;
    border-radius: 10px;
  }

  &__project-title {
    background-color: $backgroud-button;
    color: $color-text-white;
    width: 128px;
    height: 128px;
    padding: 0;
    border-radius: 8px;
    position: absolute;

    right: 20px;

    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  &__image-corner {
    position: absolute;
    top: 15px;
    right: 15px;
    height: auto;
  }
}
</style>
