<template>
  <div>
    <DisplaySwitchLink style="height: 25px; display: flex; justify-content: center;"/>
    <TheNavMenu
      :categories="categories"
      defaultCategory="All"/>
    <IndexPost 
      v-for="post in posts"
      :key="post.sys.id"
      :post="post"
      :indexPostBoxCardClass="indexPostBoxCardClass"
      :indexPostImageClass="indexPostImageClass"
      :divClass="divClass"
      class="index-post"/>
    <hr />
    <AboutMe/>
  </div>
</template>

<script>
import TheNavMenu from '~/components/TheNavMenu'
import IndexPost from '~/components/IndexPost'
import AboutMe from '~/components/AboutMe'
import DisplaySwitchLink from '~/components/DisplaySwitchLink'

const defaultCategory = 'All'

export default {
  components: { TheNavMenu, IndexPost, AboutMe, DisplaySwitchLink },

  async asyncData ({ app }) {
    const select = [
      'sys.createdAt',
      'fields.title',
      'fields.slug',
      'fields.category',
      'fields.headerImage',
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
    indexPostBoxCardClass () {
      return `width: 340px; height: 273.59px;`
    },
    indexPostImageClass () {
      return `width: 100%; height: 191.52px; object-fit: cover; display: block;`
    },
    divClass () {
      return `height: 74.34px; padding: 13.68px; font-size: 100%`
    },
  },
}
</script>

<style lang="scss" scoped>
.index-post {
  margin: 10px 5px 10px 5px;
  text-align: justify;
  display: inline-block;
}
</style>
