<template>

	<div>
		<h3>Les posts</h3>
	</div>
	<post-item class="post" v-for="post in posts" :key="post.id" :post="post" />
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
.post {
	padding: 15px;
	border: 2px solid teal;
}
</style>