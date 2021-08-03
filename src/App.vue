<template>
	<div class="container">
        <Header 
			@add-form-toggle="onAddFormToggle"
			title="ToDo List"
			:buttonStates="headerButtonStates"
		/>
		<router-view :formOpened="addFormOpened"></router-view>
		<Footer />
	</div>
</template>

<script>
import Header from "./components/Header"
import Footer from "./components/Footer"

export default {
    name: "App",
    components: {
		Header,
		Footer,
    },
    data: () => ({
		addFormOpened: false,
		headerButtonStates: {
			OnTitle: 'Add task',
			OnColor: 'green',
			OffTitle: 'Close',
			OffColor: 'black'
		}
    }),
	methods: {
		onAddFormToggle() {	
			this.addFormOpened = !this.addFormOpened;
		}
	}
};
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  padding: 30px;
}

</style>
