<template>
  <section class="project">
    <div
      class="project__background-img"
      :style="{ backgroundImage: `url(${project.image})` }"
    >
      <img class="project__image-corner-white" src="../img/corner_white.svg" />
      <h2 class="project__project-title">{{ project.title }}</h2>
      <img class="project__image-corner-blue" src="../img/corner.png" />
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

<style lang="scss">
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

  &__image-corner-blue {
    position: absolute;
    top: 15px;
    right: 15px;
    height: auto;

    @media (max-width: 480px) {
      display: none;
    }
  }

  &__image-corner-white {
    display: none;

    @media (max-width: 480px) {
      position: absolute;
      padding: 260px 0px 0px 20px;
      height: auto;
      display: block;
    }
  }

  @media (max-width: 480px) {
    &__background-img {
      &::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        height: 20%;
        background: linear-gradient(to bottom, rgba(0, 0, 0, 0), #15161c);
        border-radius: 0 0 10px 10px;
        pointer-events: none;
      }
    }

    &__project-title {
      background-color: transparent;
      color: $color-text-white;
      padding: 0;
      position: absolute;

      left: 20px;
      bottom: 10px;

      display: flex;
      justify-content: flex-start;
      align-items: center;
      text-align: left;
      font-size: $cont-size-mob;
    }
  }
}
</style>
