<template>
	<!--preventDefault avec $submit.prevent pour éviter le rechargement de la page-->
	<form @submit.prevent>
		<h4>Créer un post</h4>
		<MyInput v-model="post.title" placeholder="Nom" />
		<MyInput v-model="post.body" placeholder="Description" />
		<MyButton class="btn-create" @click="createPost">Create</MyButton>
	</form>
</template>

<script>
export default {
	emits: ['create'],
	data() {
		return {
			post: {
				title: '',
				body: '',
			}
		}
	},
	methods: {
		createPost() {
			this.post.id = Date.now()
			this.$emit('create', this.post)
			//reset form
			this.post = {
				title: '',
				body: ''
			}
		}
	},
}
</script>

<style scoped>
form {
	display: flex;
	flex-direction: column;
}

.input {
	width: 100%;
	border: 1px solid teal;
	padding: 10px 15px;
	margin-top: 15px;
}

.btn-create {
	align-self: flex-end;
	margin-top: 15px;
}
</style>
