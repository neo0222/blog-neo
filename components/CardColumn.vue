<template>
  <el-col
    :style="columnDivClass">
    <IndexPost 
      v-for="post in posts"
      :key="post.sys.id"
      :post="post"
      :indexPostBoxCardClass="indexPostBoxCardClass"
      :indexPostImageClass="indexPostImageClass"
      :divClass="divClass"
      class="index-post"/>
  </el-col>
</template>

<script>
import IndexPost from '~/components/IndexPost'

export default {
  components: { IndexPost },
  props: {
    columnDivClass: {
      type: String,
      required: true,
    },
    posts: {
      type: Array,
      required: true,
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
}
</script>


<style lang="scss" scoped>
.index-post {
  margin: 5px 5px 5px 5px;
  display: inline-block;
}
</style>