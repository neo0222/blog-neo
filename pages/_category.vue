<template>
  <div>
    <TheNavMenu
      :categories="categories"
      :defaultCategory="activeCategory"/>
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

export default {
  components: { TheNavMenu, IndexPost, AboutMe },

  data () {
    return {
      width: 0,
      height: 0,
    }
  },
  async asyncData ({ app, params }) {
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
    
    console.log(params.category)

    const posts = rawPosts.items.filter(post => post.fields.category.fields.title === params.category)
    const categories = rawPosts.includes.Entry.filter(entry => entry.sys.contentType.sys.id === 'category')

    return {
      activeCategory: params.category,
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
        return Math.min(Math.floor((this.contentWidth - 30) / 4), 342.5)
      } else if (1200>= this.contentWidth && this.contentWidth > 800) {
        return Math.floor((this.contentWidth - 20) / 3)
      } else if (800>= this.contentWidth && this.contentWidth > 600) {
        return Math.floor((this.contentWidth - 10) / 2)
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
  margin: 10px 5px 10px 5px;
  text-align: justify;
  display: inline-block;
}
</style>
