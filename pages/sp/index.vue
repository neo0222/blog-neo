<template>
  <div>
    <DisplaySwitchLink style="height: 25px; display: flex; justify-content: center;"/>
    <TheNavMenuForSp
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
import TheNavMenuForSp from '~/components/TheNavMenuForSp'
import IndexPost from '~/components/IndexPost'
import AboutMe from '~/components/AboutMe'
import DisplaySwitchLink from '~/components/DisplaySwitchLink'

const defaultCategory = 'All'

export default {
  components: { TheNavMenuForSp, IndexPost, AboutMe, DisplaySwitchLink },

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
      return `width: 85vw;`
    },
    indexPostImageClass () {
      return `width: 85vw; object-fit: cover; display: block;`
    },
    divClass () {
      return `padding: 4vw; font-size: 100%`
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
