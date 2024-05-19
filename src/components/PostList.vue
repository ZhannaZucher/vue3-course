<template>

	<div v-if="posts.length > 0">
		<h3 class="posts-header">Les posts</h3>
		<TransitionGroup name="list">
			<PostItem v-for="post in posts" :key="post.id" :post="post" @remove="$emit('remove', post)" />
		</TransitionGroup>
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

/*styles for transition-group*/
.list-item {
	display: inline-block;
	margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
	transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
	opacity: 0;
	transform: translateX(130px);
}

/** -move animates reordering posts list on sort select */
.list-move {
	transition: transform 0.8s ease;
}
</style>