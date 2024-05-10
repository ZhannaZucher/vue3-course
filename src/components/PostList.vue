<template>

	<div v-if="posts.length > 0">
		<h3 class="posts-header">Les posts</h3>
		<post-item v-for="post in posts" :key="post.id" :post="post" @remove="$emit('remove', post)" />
	</div>
	<h3 v-else>Il n'y a pas de posts</h3>

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