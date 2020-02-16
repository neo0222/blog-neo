<template>
  <el-card :body-style="{ padding: '0px' }" :style="indexPostBoxCardClass">
    <el-image
      :src="post.fields.headerImage.fields.file.url"
      :style="indexPostImageClass"/>
    <div :style="divClass">
      <h4 class="post-head">
        <nuxt-link :to="{ name: 'slug', params: { slug: post.fields.slug }}" class="post-head__title">{{ post.fields.title }}</nuxt-link>
      </h4>
      <div class="post-date">
        <time :datetime="post.sys.createdAt">{{ displayCreatedAt }}</time>
      </div>

    </div>
  </el-card>
</template>

<script>
import dateformat from 'dateformat'

export default {
  props: {
    post: {
      type: Object,
      required: true
    },
    indexPostBoxCardClass: {
      type: String,
      required: true
    },
    indexPostImageClass: {
      type: String,
      required: true,
    },
    divClass: {
      type: String,
      required: true
    }
  },

  computed: {
    displayCreatedAt () {
      return dateformat(new Date(this.post.sys.createdAt), 'yyyy-mm-dd')
    },

    renderedContent () {
      return this.$md.render(this.post.fields.content)
    }
  }
}
</script>

<style lang="scss" scoped>

html {
  font-size: 100%;
}

.post-head {
  font-size: 1.5rem;
  margin-bottom: 4px;

  &__title {
    color: inherit;

    &:hover {
      opacity: 0.8;
    }
  }
}

.post-date {
  font-size: 1.2rem;
  margin-bottom: 4px;

  &__title {
    color: inherit;

    &:hover {
      opacity: 0.8;
    }
  }
}


// .box-card {
//   width: 300px;
//   height: 250px;
// }
</style>
