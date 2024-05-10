<template>

	<div>
		<h3 class="posts-header">Les posts</h3>
	</div>
	<post-item v-for="post in posts" :key="post.id" :post="post" @remove="$emit('remove', post)" />
</template>

<script>
import PostItem from './PostItem.vue';

export default {
	components: {
		PostItem
	},
	props: {
		posts: {
			type: Array,
			required: true
		}
	}
}
</script>

<style scoped>
.posts-header {
	margin-bottom: 15px;
}
</style>