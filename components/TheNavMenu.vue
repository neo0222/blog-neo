<template>
    <el-menu
			:default-active="defaultCategory"
			mode="horizontal"
			@select="handleSelect"
			class="nav-menu">
			<el-menu-item
				index="All">
				<nuxt-link :to="{ name: 'index' }">All</nuxt-link>
			</el-menu-item>
			<el-menu-item
				v-for="category in categories"
				:key="category.sys.id"
				:index="category.fields.title">
				<nuxt-link
					:to="{ name: 'category', params: { category: category.fields.title }}">
					{{ category.fields.title }}
				</nuxt-link>
			</el-menu-item>
		</el-menu>
</template>

<script>
export default {
  props: {
    categories: {
      type: Array,
      required: true
		},
		defaultCategory: {
			type: String,
			required: true
		}
	},
	methods: {
		handleSelect(index) {
			this.$parent.activeCategory = index
		},
	},
}
</script>

<style lang="scss" scoped>
.el-menu {
	display: flex;
	justify-content: center;
}

.el-menu-item {
	display: flex;
	justify-content: center;
}
</style>
