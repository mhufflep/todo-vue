<template>
    <div class="container">
        <Header 
			@add-form-toggle="onAddFormToggle"
			title="ToDo List"
			:buttonStates="headerButtonStates"
		/>
        <AddTask
			v-if="addFormOpened" 
			@add-task="onAddTask"
		/>
		<Tasks
			@delete-task="onDeleteTask"
			@toggle-reminder="onToggleReminder"
			:tasks="tasks"
		/>
    </div>
</template>

<script>
import Header from "./components/Header"
import Tasks from "./components/Tasks"
import AddTask from "./components/AddTask"

export default {
    name: "App",
    components: {
		AddTask,
        Header,
        Tasks,
    },
    data: () => ({
		addFormOpened: false,
		tasks: [],
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
		},
		onDeleteTask(id) {
			if (confirm('are you sure?'))
			{
				this.tasks = this.tasks.filter(
					(task) => task.id !== id
				);
			}
		},
		onToggleReminder(id) {
			this.tasks.forEach((task) => {
				if (task.id === id)
					task.reminder = !task.reminder;
			});
		},
		async onAddTask(newTask) {
			const res = await fetch(`/api/tasks`, {
				method: "POST",
				headers: {
					'Content-type': "application/json"
				},
				body: JSON.stringify(newTask)
			});

			const data = await res.json();
			this.tasks.push(data);
		},
		async fetchTasks() {
			const res = await fetch('/api/tasks');
			const data = await res.json();
			return data
		},
		async fetchTask(id) {
			const res = await fetch(`/api/tasks/${id}`);
			const data = await res.json();
			return data
		}
	},
    async created() {
        this.tasks = await this.fetchTasks()
    },
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
