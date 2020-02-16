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
        <li>Go</li>
        <li>Kubernetes</li>
        <li>Terraform</li>
        <li>AWS</li>
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
        <a href="https://www.instagram.com/neostagram0222/" target="_blank" rel="nofollow noreferrer">Instagram @neostagram0222</a>
      </li>
    </ul>

    <p>This blog source code is on GitHub (<a href="https://github.com/neo0222/blog-neo" target="_blank" rel="nofollow noopener">neo0222/blog-neo</a>)</p>

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
