<template>
  <div class="app-container">
    <header>
      <div class="site-title">
        <nuxt-link :to="{ name: 'index' }" exact class="site-title__link">Neo Blog</nuxt-link>
      </div>
    </header>
  </div>
</template>

<style lang="scss" scoped>
.app-container {
  max-width: 1000px;
  margin-right: auto;
  margin-left: auto;
  padding: 20px 20px 0px 20px;
}

.site-title {
  font-size: 3.0rem;
  line-height: 1.3;
  font-weight: bold;
  text-align: center;

  &__link {
    color: inherit;
    opacity: 1;

    &:hover {
      opacity: .9;
    }
  }
}

.site-description {
  margin-top: 5px;
  text-align: center;
}

.main {
  margin-top: 30px;
}

.content {
  max-width: 800px;
  margin-right: auto;
  margin-left: auto;
}
</style>
