<template>
	<div class="app">
		<h1>Posts app</h1>
		<div class="create-form">
			<my-button @click="showModal">Créer un post</my-button>
		</div>
		<my-modal v-model:show="modalVisible">
			<post-form @create="createPost" />
		</my-modal>
		<post-list v-if="!isLoading" :posts="posts" @remove="removePost" />
		<div v-else>Is Loading...</div>
	</div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import axios from 'axios'

export default {
	components: {
		PostList, PostForm
	},
	data() {
		return {
			posts: [],
			modalVisible: false,
			isLoading: false
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
		},
		async fetchPosts() {
			try {
				this.isLoading = true
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
				this.posts = response.data
				console.log(response);
			} catch (error) {
				alert('Server error')
			} finally {
				this.isLoading = false
			}
		},
	},
	mounted() {
		this.fetchPosts()
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