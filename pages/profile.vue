<template>
  <div>
    <h1>About me</h1>
    <div class="profile-descriptions">
      <div>Name: neo</div>
      <div>Job: Software Engineer</div>
    </div>

    <h2>Loves</h2>
    <div class="profile-descriptions">
      <ul>
        <li>AWS</li>
        <li>Javascript(node.js, vue.js etc...)</li>
        <li>Block Chain</li>
        <li>Tea!</li>
      </ul>
    </div>

    <h2>Links</h2>
    <ul>
      <li>
        <a href="https://qiita.com/neo0222" target="_blank" rel="nofollow noreferrer">Qiita @neo0222</a>
      </li>
      <li>
        <a href="https://github.com/neo0222" target="_blank" rel="nofollow noreferrer">GitHub @neo0222</a>
      </li>
      <li>
        <a href="https://twitter.com/neostagram0222" target="_blank" rel="nofollow noreferrer">Instagram @neostagram0222</a>
      </li>
    </ul>

    
  </div>
</template>

<script>
export default {
  head () {
    return {
      title: 'About me',
      meta: [
        { hid: 'og:title', property: 'og:title', content: 'About me' },
        { hid: 'og:description', property: 'og:description', content: 'About me' }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.profile-descriptions {
  margin-bottom: 20px;
  > * {
    margin-bottom: 8px;
  }
}
</style>
