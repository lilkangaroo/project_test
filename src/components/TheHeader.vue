<template>
  <article class="top">
    <header class="header">
      <img class="header__logo" src="@/img/logo.png" alt="logo" />
      <div class="header__nav">
        <nav class="header__nav" @click.prevent>
          <a href="#" class="header__item">Агенство</a>
          <a href="#" class="header__item">Услуги</a>
          <a href="#" class="header__item">Кейсы</a>
          <a href="#" class="header__item">Блог</a>
          <a href="#" class="header__item">Контакты</a>
        </nav>
      </div>
    </header>
  </article>
</template>

<script></script>

<style lang="scss">
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  &__logo {
    margin-right: 200px;
    align-self: left;
  }

  &__nav {
    display: flex;
    flex-grow: 1;
    gap: 50px;
  }

  &__item {
    transition:
      color 0.8s ease,
      transform 0.5s ease;

    &:hover {
      color: $color-nav-hover;
      transform: scale(1.2);
    }
  }
}
</style>
