<template>
	<div class="page__wrapper">
		<div v-for="pageNumber in totalPages" :key="pageNumber" class="page"
			:class="{ 'current-page': page === pageNumber }" @click="changePage(pageNumber)">{{ pageNumber }}</div>
	</div>
</template>

<script>
export default {
	props: {
		totalPages: {
			type: Number,
			required: true
		},
		page: {
			type: Number,
			required: true
		},
	},
	methods: {
		changePage(pageNumber) {
			this.$emit('change', pageNumber)
		}
	}

}
</script>

<style scoped>
.page__wrapper {
	display: flex;
	margin-top: 15px;
}

.page {
	border: 1px solid black;
	padding: 10px;
}

.current-page {
	border: 2px solid teal;
	font-weight: bold;
	color: teal
}
</style>