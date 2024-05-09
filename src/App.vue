<template>
	<div class="app">
		<form>
			<h4>Création d'un post</h4>
			<input v-bind:value="title" @input="inputTitle" class="input" type="text" placeholder="Nom">
			<input v-bind:value="body" @input="inputBody" class="input" type="text" placeholder="Description">
			<button class="btn" @click="createPost">Créer un post</button>
			<p>Le titre sera : {{ title }}</p>
		</form>
		<div class="post" v-for="post in posts" :key="post.id">
			<div><strong>Nom: </strong>{{ post.title }}</div>
			<div><strong>Description: </strong>{{ post.body }}</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			posts: [
				{ id: 1, title: 'Javascript 1', body: 'Je suis un post sur JS' },
				{ id: 2, title: 'Javascript 2', body: 'Je suis un post sur JS' },
				{ id: 3, title: 'Javascript 3', body: 'Je suis un post sur JS' },
			],
			title: '',
			body: ''
		}
	},
	methods: {
		createPost() {

		},
		inputTitle(event) {
			this.title = event.target.value
		},
		inputBody(event) {
			this.body = event.target.value
		}
	}
}
</script>

<style>
* {
	padding: 0;
	margin: 15px 0 0 0;
	box-sizing: border-box;
}

.app {
	padding: 20px;
}

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

.btn {
	margin-top: 15px;
	align-self: flex-end;
	padding: 10px 15px;
	background: none;
	color: teal;
	border: 1px solid teal;
}

.post {
	padding: 15px;
	border: 2px solid teal;
}
</style>