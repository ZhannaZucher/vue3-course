<template>
	<div class="app">
		<h1>Posts app</h1>
		<div class="create-form">
			<my-button @click="showModal">Créer un post</my-button>
			<my-select v-model="selectedSort" :options="sortOptions"></my-select>
		</div>
		<my-modal v-model:show="modalVisible">
			<post-form @create="createPost" />
		</my-modal>
		<post-list v-if="!isLoading" :posts="sortedPosts" @remove="removePost" />
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
			isLoading: false,
			selectedSort: '',
			sortOptions: [
				{ value: 'title', name: 'Titre' },
				{ value: 'body', name: 'Contenu' },
			]
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
				console.log(response.data);
			} catch (error) {
				alert('Server error')
			} finally {
				this.isLoading = false
			}
		},
	},
	mounted() {
		this.fetchPosts()
	},
	computed: {
		sortedPosts() {
			//we sort the new array not the original one
			return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
		}
	},
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
	display: flex;
	justify-content: space-between;
}
</style>