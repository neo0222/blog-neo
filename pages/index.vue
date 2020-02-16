<template>
  <div>
    <TheNavMenu
      :categories="categories"/>
    <IndexPost 
      v-for="post in displayedPosts"
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

const defaultCategory = 'All'

export default {
  components: { TheNavMenu, IndexPost, AboutMe },

  data () {
    return {
      activeCategory: defaultCategory,
      width: 0,
      height: 0,
    }
  },
  async asyncData ({ app }) {
    const select = [
      'sys.id',
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
    displayedPosts () {
      return this.activeCategory === defaultCategory ?
        this.posts : this.posts.filter(post => post.fields.category.fields.title === this.activeCategory)
    },
    contentWidth () {
      return this.width - 40
    },
    indexPostBoxCardClass () {
      return `width: ${this.cardWidth}px; height: ${this.cardHeight}px;`
    },
    indexPostImageClass () {
      return `width: 100%; height: ${this.headerImageHeight}px; object-fit: cover; display: block;`
    },
    divClass () {
      return `height: ${this.cardHeight - this.headerImageHeight}; padding: ${this.cardHeight / 20}px; font-size: 100%`
    },
    cardWidth () {
      if (this.contentWidth > 1200) {
        return Math.min(Math.floor((this.contentWidth - 40) / 4), 340)
      } else if (1200>= this.contentWidth && this.contentWidth > 800) {
        return Math.floor((this.contentWidth - 30) / 3)
      } else if (800>= this.contentWidth && this.contentWidth > 600) {
        return Math.floor((this.contentWidth - 20) / 2)
      } else {
        return (this.contentWidth - 10)
      }
      
    },
    cardHeight () {
      return this.cardWidth * 0.8
    },
    headerImageHeight () {
      return this.cardHeight * 0.7
    },
  },
  methods: {
    handleResize: function() {
      if (process.browser) {
        // resizeのたびにこいつが発火するので、ここでやりたいことをやる
        this.width = window.innerWidth;
        this.height = window.innerHeight;
      }
      
    }
  },
  mounted: function () {
    if (process.browser) {
      window.addEventListener('resize', this.handleResize)
      this.width = window.innerWidth
      this.height =  window.innerHeight
    }
  },
  beforeDestroy: function () {
    if (process.browser) {
      window.removeEventListener('resize', this.handleResize)
    }
    
  }
}
</script>

<style lang="scss" scoped>
.index-post {
  margin: 5px 5px 5px 5px;
  display: inline-block;
}
</style>
