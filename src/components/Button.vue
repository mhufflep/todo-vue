<template>
	<button
		:style="{background: color}"
		@click="$emit('btn-clicked')"
	>{{ text }}</button>
</template>

<script>
export default {
	name: 'Button',
	props: {
		text: {
			type: String,
			default: 'Click'
		},
		color: {
			type: String,
			default: '#000'
		}
	}
}
</script>

<style scoped>
	button {
		background: #000;
		color: #fff;
		border: none;
		padding: 10px 20px;
		margin: 10px;
		border-radius: 5px;
		font-size: 1rem;
	}
	button:focus {
		outline: none;
	}
</style>