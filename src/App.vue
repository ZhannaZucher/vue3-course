<template>
	<div class="app">
		<h1>Posts app</h1>
		<div class="create-form">
			<my-button @click="showModal">Créer un post</my-button>
		</div>
		<my-modal v-model:show="modalVisible">
			<post-form @create="createPost" />
		</my-modal>
		<post-list :posts="posts" @remove="removePost" />
	</div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'

export default {
	components: {
		PostList, PostForm
	},
	data() {
		return {
			posts: [
				{ id: 1, title: 'Javascript 1', body: 'Je suis un post sur JS' },
				{ id: 2, title: 'Javascript 2', body: 'Je suis un post sur JS' },
				{ id: 3, title: 'Javascript 3', body: 'Je suis un post sur JS' },
			],
			modalVisible: false
		}
	},
	methods: {
		createPost(post) {
			this.posts.push(post)
			this.modalVisible = false
		},
		removePost(post) {
			this.posts = this.posts.filter(p => p.id !== post.id)
		},
		showModal() {
			this.modalVisible = true
		}
	}
}
</script>

<style>
* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
}

.app {
	padding: 20px;
}

h1,
.create-form {
	margin: 15px 0;
}
</style>