<template>
  <div>
    <IndexPost v-for="post in displayedPosts" :key="post.sys.id" :post="post" class="index-post"/>

    <hr />
    <AboutMe/>
  </div>
</template>

<script>
import IndexPost from '~/components/IndexPost'
import AboutMe from '~/components/AboutMe'

const defaultCategory = 'All'

export default {
  components: { IndexPost, AboutMe },

  data () {
    return {
      activeCategory: defaultCategory,
    }
  },
  async asyncData ({ app }) {
    const select = [
      'sys.createdAt',
      'fields.title',
      'fields.slug',
      'fields.category',
    ]

    const rawPosts = await app.$contentful.getEntries({
        content_type: 'post',
        order: '-sys.createdAt',
        select: select.join(',')
      })
    
    const posts = rawPosts.items
    const categories = rawPosts.includes.Entry.filter(entry => entry.sys.contentType.sys.id === 'category')

    return {
      posts: posts,
      categories: categories,
    }
  },

  head () {
    return {
      titleTemplate: null
    }
  },

  computed: {
    displayedPosts () {
      return this.posts.filter(post => post.fields.category.fields.title === this.activeCategory)
    }
  }
}
</script>

<style lang="scss" scoped>
.index-post {
  margin-top: 24px;
}
</style>
