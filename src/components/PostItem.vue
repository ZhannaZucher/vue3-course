<template>
	<div class="post">
		<div>
			<div>{{ post.id }}</div>
			<div><strong>Nom: </strong>{{ post.title }}</div>
			<div><strong>Description: </strong>{{ post.body }}</div>
		</div>
		<div class="post__btns">
			<MyButton @click="$emit('remove', post)">Delete</MyButton>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		post: {
			type: Object,
			required: true,
		}
	}
}
</script>

<style scoped>
.post {
	padding: 15px;
	margin-bottom: 15px;
	border: 2px solid teal;
	display: flex;
	align-items: center;
	justify-content: space-between;
}
</style>