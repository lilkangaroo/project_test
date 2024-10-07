<template>
  <footer class="footer">
    <div class="footer__container">
      <section class="org">
        <img class="org__logofooter" src="@/img/logo_footer.png" />
        <p class="org__desc">
          Веб-разработка и <br />
          усиление IT-команд
        </p>
      </section>
      <div class="cont-nav-wrapper">
        <section class="contacts">
          <p class="contacts__item">+7 999 123 45 67</p>
          <p class="contacts__item">hello@cyberia.studio</p>
          <p class="contacts__item">ул.Ярных, д.35, оф.10</p>
        </section>
        <section class="navigation">
          <nav class="navigation__nav">
            <a href="#" class="navigation__item">Агенство</a>
            <a href="#" class="navigation__item">Услуги</a>
            <a href="#" class="navigation__item">Кейсы</a>
            <a href="#" class="navigation__item">Блог</a>
            <a href="#" class="navigation__item">Контакты</a>
          </nav>
        </section>
      </div>
    </div>
  </footer>
</template>
<script></script>

<style lang="scss">
.footer {
  background-color: $backgroud-button;
  padding: 100px 0 100px 200px;

  &__container {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 100px;
  }
}

.cont-nav-wrapper {
  display: flex;
  flex-direction: row;
  gap: 100px;
}

.contacts {
  display: flex;
  flex-direction: column;
}

.navigation {
  display: flex;
  flex-direction: column;
  gap: 10px;

  &__nav {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  &__item {
    width: calc(30% - 10px);
    padding: 10px 0px;
    margin: 0 10px;
  }
}
</style>
