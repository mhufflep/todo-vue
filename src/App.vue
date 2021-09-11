<template>
	<div class="app-wrap">
		<div class="container">
	        <Header 
				@add-form-toggle="onAddFormToggle"
				title="ToDo List"
				:buttonStates="headerButtonStates"
			/>
			<router-view :formOpened="addFormOpened"></router-view>
			<Footer />
		</div>
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
			OnColor: '#2e772e',
			OffTitle: 'Close',
			OffColor: '#3f3f3f'
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

.app-wrap {
	display: flex;
	justify-content: center;
	align-content: center;
	width: 100%;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
	width: 40vw;
	background-color: rgb(233, 233, 233);
	border: 1px solid gray;
	border-radius: 5px;
	padding: 10px;
}

</style>
