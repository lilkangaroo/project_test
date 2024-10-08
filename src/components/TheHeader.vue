<template>
  <article class="top">
    <header class="header">
      <img class="header__logo" src="@/img/logo.png" alt="logo" />
      <div class="header__nav">
        <nav class="header__nav-items">
          <ul>
            <li><a href="#" class="header__item">Агенство</a></li>
            <li><a href="#" class="header__item">Услуги</a></li>
            <li><a href="#" class="header__item">Кейсы</a></li>
            <li><a href="#" class="header__item">Блог</a></li>
            <li><a href="#" class="header__item">Контакты</a></li>
          </ul>
        </nav>
      </div>
      <!-- Кнопка меню для мобильной версии -->
      <button class="header__menu-button" @click="toggleMenu">
        <span class="header__bar"></span>
        <span class="header__bar"></span>
        <span class="header__bar"></span>
      </button>
      <!-- Мобильное меню -->
      <div
        class="header__menu"
        :class="{ 'header__menu--active': isMenuActive }"
      >
        <button class="header__close-button" @click="toggleMenu">✖</button>
        <nav class="header__nav-items">
          <ul>
            <li><a href="#" class="header__item">Агенство</a></li>
            <li><a href="#" class="header__item">Услуги</a></li>
            <li><a href="#" class="header__item">Кейсы</a></li>
            <li><a href="#" class="header__item">Блог</a></li>
            <li><a href="#" class="header__item">Контакты</a></li>
          </ul>
        </nav>
        <hr class="header__divider" />
        <div class="header__contacts">
          <h4>Контакты:</h4>
          <p>+7 999 123 45 67</p>
          <p>hello@cyberia.studio</p>
          <p>ул.Ярных, д.35, оф.10</p>
        </div>
        <hr class="header__divider" />
      </div>
    </header>
  </article>
</template>

<script>
export default {
  data() {
    return {
      isMenuActive: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuActive = !this.isMenuActive;
    },
  },
};
</script>

<style lang="scss">
.header {
  width: 100%;
  padding: 50px 200px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  overflow: hidden;

  &__logo {
    margin-right: 200px;
    align-self: flex-start;

    @media (max-width: 480px) {
      margin: 30px 0 30px 20px;
      width: 100px;
      height: auto;
    }
  }

  &__nav {
    display: flex;
    flex-grow: 1;

    ul {
      display: flex;
      gap: 50px;
      list-style: none;
      padding: 0;
      margin: 0;

      li {
        margin: 0;
      }
    }

    @media (max-width: 480px) {
      display: none;
    }
  }

  &__menu-button {
    display: none;

    @media (max-width: 480px) {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      width: 50px;
      height: 40px;
      background: transparent;
      border: none;
      margin-right: 20px;
    }
  }

  &__bar {
    display: block;
    width: 100%;
    height: 1.5px;
    background-color: $color-text;
    margin: 2px 0;
  }

  &__menu {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: $color-header;
    z-index: 1000;
    display: none;
    flex-direction: column;
    padding: 20px;
    overflow-y: auto;
    box-sizing: border-box;

    &--active {
      display: flex;
    }

    @media (min-width: 481px) {
      display: none;
    }
  }

  &__close-button {
    background: transparent;
    border: none;
    color: $color-text;
    font-size: 24px;
    align-self: flex-end;
    margin-bottom: 10px;
    margin-top: 10px;

    @media (min-width: 481px) {
      display: none;
    }
  }

  &__nav-items {
    ul {
      padding: 0;
      list-style: none;
      margin: 0;

      li {
        font-size: $menu-size-mob;
        margin: 30px 0;
      }

      a {
        color: $color-text;
        text-decoration: none;
      }
    }
  }

  &__divider {
    border: none;
    border-top: 1px solid $color-sep;
    margin: 20px;
  }

  &__contacts {
    color: $color-cont-mob;
    text-align: left;
    box-sizing: border-box;
    margin-bottom: 10px;

    h4 {
      font-size: $menu-size-mob;
      margin-bottom: 50px;
    }

    p {
      font-size: $cont-size-mob;
    }

    @media (min-width: 481px) {
      display: none;
    }
  }

  @media (max-width: 480px) {
    padding: 0;
    width: 100%;
    align-items: center;
    background-color: $color-header;

    &__logo {
      margin: 30px 0px 30px 20px;
      align-self: flex-start;
      width: 100px;
      height: auto;
    }
  }
}
</style>
