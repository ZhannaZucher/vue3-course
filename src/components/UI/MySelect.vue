<template>
	<select :value="modelValue" @change="changeOption">
		<option disabled value="">Choisir une option</option>
		<option v-for="option in options" :key="option.value" :value="option.value">{{ option.name }}</option>
	</select>
</template>

<script>
export default {
	name: 'MySelect',
	emits: ['update:model-value'],
	props: {
		modelValue: {
			type: String
		},
		options: {
			type: Array,
			default: () => []
		},
	},
	methods: {
		changeOption(event) {
			this.$emit('update:modelValue', event.target.value)
		}
	}
}
</script>

<style scoped></style>