<template>
  <div class="app-container">
    <main class="main">
      <div class="content">
        <slot/>
      </div>
    </main>
  </div>
</template>

<style lang="scss" scoped>
.app-container {
  max-width: 1440px;
  margin-right: auto;
  margin-left: auto;
  padding: 0px 20px 20px 20px;
}

.site-title {
  font-size: 4.6rem;
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
  margin-top: 0px;
}

.content {
  max-width: 1500px;
  margin-right: auto;
  margin-left: auto;
}
</style>
