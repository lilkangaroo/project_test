<template>
  <article class="top">
    <header class="header">
      <img class="header__logo" src="@/img/logo.png" alt="logo" />
      <nav class="header__nav" @click.prevent>
        <a href="#" class="header__item">Агенство</a>
        <a href="#" class="header__item">Услуги</a>
        <a href="#" class="header__item">Кейсы</a>
        <a href="#" class="header__item">Блог</a>
        <a href="#" class="header__item">Контакты</a>
      </nav>
    </header>
  </article>
</template>

<script></script>

<style lang="scss">
.header {
  display: flex;
  background-color: #24252f;
  align-items: center;
  justify-content: space-between;

  &__logo {
    margin-right: 200px;
    align-self: left;
  }

  &__nav {
    display: flex;
    flex-grow: 5;
    gap: 50px;
  }

  &__item {
    color: $color-text;
    text-decoration: none;
    transition: color 0.3s ease;

    &:hover {
      color: $color-nav-hover;
    }
  }
}
</style>
