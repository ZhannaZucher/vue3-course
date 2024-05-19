<template>
	<div class="app">
		<h1>Posts app</h1>
		<MyInput v-model="searchQuery" placeholder="Rechercher par titre..." />
		<div class="create-form">
			<MyButton @click="showModal">Créer un post</MyButton>
			<MySelect v-model="selectedSort" :options="sortOptions"></MySelect>
		</div>
		<MyModal v-model:show="modalVisible">
			<PostForm @create="createPost" />
		</MyModal>
		<PostList v-if="!isLoading" :posts="sortedAndSearhedPosts" @remove="removePost" />
		<div v-else>Is Loading...</div>
		<PostPagination :totalPages="totalPages" :page="page" @change="goToPage" />
	</div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import PostPagination from '@/components/PostPagination'
import axios from 'axios'

export default {
	components: {
		PostList, PostForm, PostPagination
	},
	data() {
		return {
			posts: [],
			modalVisible: false,
			isLoading: false,
			selectedSort: '',
			searchQuery: '',
			page: 1,
			limitPostsPerPage: 10,
			totalPages: 0,
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
		goToPage(pageNumber) {
			this.page = pageNumber
		},
		async fetchPosts() {
			try {
				this.isLoading = true
				//with params url will be :https://jsonplaceholder.typicode.com/posts?_page=1&_limit=10
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
					params: {
						_page: this.page,
						_limit: this.limitPostsPerPage
					}
				})
				//calculating total number of pages (the API return 100 posts)
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limitPostsPerPage)
				this.posts = response.data
				// console.log(response.data);
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
		},
		sortedAndSearhedPosts() {
			return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
		}
	},
	watch: {
		page() {
			this.fetchPosts()
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
	display: flex;
	justify-content: space-between;
}
</style>