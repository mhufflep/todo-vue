<template>
  <header>
  	<h1>{{ title }}</h1>
    <Button
		@click="onClick()"
		:text="text"
		:color="color"
		v-show="isHome"
	/>
  </header>
</template>

<script>
import { createTextVNode } from 'vue'
import Button from './Button'

export default {
	name: 'Header',
	components: {
		Button,
	},
	data: () => ({
		buttonOn: true,
		text: '',
		color: '',
	}),
	methods: {
		onClick() {
			this.buttonOn = !this.buttonOn;
			this.text = this.buttonOn ? this.buttonStates.OnTitle : this.buttonStates.OffTitle;
			this.color = this.buttonOn ? this.buttonStates.OnColor : this.buttonStates.OffColor;
			this.$emit('add-form-toggle');
		}
	},
	props: {
		title: String,
		buttonStates: Object,
	},
	created() {		
		this.text = this.buttonStates.OnTitle; 
		if (this.text === null)
		{
			this.text = buttonOn ? 'Button on' : 'Button off';
		}

		this.color = this.buttonStates.OnColor; 
		if (this.color === null)
		{
			this.color = buttonOn ? 'green' : 'black';
		}
	},
	computed: {
		isHome() {
			return (this.$route.path === '/');
		}
	}
}
</script>

<style scoped>
	header {
		font-size: 1rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
    	margin: 20px;
	}
</style>