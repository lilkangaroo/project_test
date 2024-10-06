<template>
  <article class="top">
    <header class="header">
      <img class="logo" src="@/img/logo.png" alt="logo" />
      <nav class="nav" @click.prevent>
        <a href="#" class="menu-item">Агенство</a>
        <a href="#" class="menu-item">Услуги</a>
        <a href="#" class="menu-item">Кейсы</a>
        <a href="#" class="menu-item">Блог</a>
        <a href="#" class="menu-item">Контакты</a>
      </nav>
    </header>
  </article>
</template>

<script></script>

<style>
.header {
  height: 100px;
  background-color: #24252f;
}

.menu-item {
  padding: 30px;
  text-decoration: none;
  color: #ffffff;
}
</style>
