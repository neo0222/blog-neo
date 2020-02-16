<template>
  <div>
    <div class="profile-head">
      <nuxt-link :to="{ name: 'profile' }">About me</nuxt-link>
    </div>
    <div class="profile-body">{{ aboutMe }}</div>

    <ul>
      <li>
        <a href="https://qiita.com/neo0222" target="_blank" rel="nofollow noreferrer">Qiita @neo0222</a>
      </li>
      <li>
        <a href="https://github.com/neo0222" target="_blank" rel="nofollow noreferrer">GitHub @neo0222</a>
      </li>
      <li>
        <a href="https://www.instagram.com/neostagram0222/" target="_blank" rel="nofollow noreferrer">Instagram @neostagram0222</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  computed: {
    aboutMe () {
      return { name: 'neo', job: 'Software Engineer' }
    }
  }
}
</script>

<style lang="scss" scoped>
.profile-head {
  font-size: 2rem;
}

.profile-body {
  margin-top: 6px;
}
</style>
