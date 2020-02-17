<template>
  <div>
    <TheNavMenu
      :categories="categories"/>
    <el-col style="padding-bottom: 20px">
      <CardColumn
        :columnDivClass="columnDivClass"
        :posts="firstColumn"
        :indexPostBoxCardClass="indexPostBoxCardClass"
        :indexPostImageClass="indexPostImageClass"
        :divClass="divClass"/>
      <CardColumn
        :columnDivClass="columnDivClass"
        :posts="secondColumn"
        :indexPostBoxCardClass="indexPostBoxCardClass"
        :indexPostImageClass="indexPostImageClass"
        :divClass="divClass"/>
      <CardColumn
        :columnDivClass="columnDivClass"
        :posts="thirdColumn"
        :indexPostBoxCardClass="indexPostBoxCardClass"
        :indexPostImageClass="indexPostImageClass"
        :divClass="divClass"/>
      <CardColumn
        :columnDivClass="columnDivClass"
        :posts="fourthColumn"
        :indexPostBoxCardClass="indexPostBoxCardClass"
        :indexPostImageClass="indexPostImageClass"
        :divClass="divClass"/>
    </el-col>
    <div>
      <hr />
    </div>
    <AboutMe/>
  </div>
</template>

<script>
import TheNavMenu from '~/components/TheNavMenu'
import AboutMe from '~/components/AboutMe'
import CardColumn from '~/components/CardColumn'

const defaultCategory = 'All'
// カードの表示領域の上限は画面幅1440pxに最適化されたもの。
// それ以上大きい画面で表示してもカードが大きくならないようカード幅にも上限を設定する。
const maxWidthOfCard = 340

export default {
  components: { TheNavMenu, AboutMe, CardColumn },

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
    filteredPostsByCategory () {
      return this.activeCategory === defaultCategory ?
        this.posts : this.posts.filter(post => post.fields.category.fields.title === this.activeCategory)
    },
    contentWidth () {
      return this.width - 40
    },
    indexPostBoxCardClass () {
      return `width: ${this.cardWidth}px;`
    },
    indexPostImageClass () {
      return 'width: 100%; object-fit: cover; display: block;'
    },
    divClass () {
      // 記事説明欄のpaddingはカード幅に比例
      return `padding: ${this.cardWidth / 25}px; font-size: 100%`
    },
    columnDivClass () {
      // カードの間隔は10px
      return `width: ${this.cardWidth + 10}px; height: auto; float: left;`
    },
    cardWidth () {
      // 間隔の分差し引く
      return Math.min(Math.floor(this.cardColumnWidth - 10), maxWidthOfCard)
    },
    cardColumnWidth () {
      // カードの幅はカードを何列並べるかで決まる
      return this.contentWidth / this.numberOfColumns
    },
    numberOfColumns() {
      // カードの列数はウィンドウの幅で決まる
      if (this.contentWidth > 1050) {
        return 4
      } else if (1050>= this.contentWidth && this.contentWidth > 800) {
        return 3
      } else if (800>= this.contentWidth && this.contentWidth > 600) {
        return 2
      } else {
        return 1
      }
      
    },
    // カードを左上から順に詰めていきたいので、表示対象を順に各列に割り振っていく
    firstColumn () {
      // 1列目
      return this.filteredPostsByCategory.filter((el, index) => {
        return index % this.numberOfColumns === 0
      })
    },
    secondColumn () {
      // 2列目（画面幅が640px未満だと要素0）
      return this.filteredPostsByCategory.filter((el, index) => {
        return index % this.numberOfColumns === 1
      })
    },
    thirdColumn () {
      // 3列目（画面幅が840px未満だと要素0）
      return this.filteredPostsByCategory.filter((el, index) => {
        return index % this.numberOfColumns === 2
      })
    },
    fourthColumn () {
      // 4列目（画面幅が1090px未満だと要素0）
      return this.filteredPostsByCategory.filter((el, index) => {
        return index % this.numberOfColumns === 3
      })
    },
  },
  // 以下、画面サイズ取得関連処理
  methods: {
    handleResize: function() {
      if (process.browser) {
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

