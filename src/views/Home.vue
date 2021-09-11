<template>
	<AddTask
		v-if="formOpened" 
		@add-task="onAddTask"
	/>
	<Tasks
		@delete-task="onDeleteTask"
		@toggle-reminder="onToggleReminder"
		:tasks="tasks"
	/>	
</template>

<script>
import Tasks from "../components/Tasks"
import AddTask from "../components/AddTask"

export default {
	name: 'Home',
	components: {
		Tasks,
		AddTask,
	},
	props: {
		formOpened: Boolean,
	},
	data: () => ({
		tasks: []
	}),
	methods: {
		onAddFormToggle() {	
			this.addFormOpened = !this.addFormOpened;
		},
		async onDeleteTask(id) {
			if (confirm('are you sure?')) {
				const res = await fetch(`api/tasks/${id}`, {
					method: 'DELETE',
				});
	
				if (res.status === 200) {		
					this.tasks = this.tasks.filter((task) =>
						task.id !== id
					);
				} 
				else {
					alert(`deleting task with id: ${id} failed`);
				}
			}
		},
		async updateTask(updTask) {
			const res = await fetch(`/api/tasks/${updTask.id}`, {
				method: "PUT",
				headers: {
					'Content-type': 'application/json'
				},
				body: JSON.stringify(updTask)
			})

			const data = await res.json();
			return data;
		},
		async onToggleReminder(id) {
			const oldTask = await this.fetchTask(id);
			const updTask = {...oldTask, reminder: !oldTask.reminder};
			const resTask = await this.updateTask(updTask);
			
			this.tasks.forEach((task) => {
				if (task.id === id)		
					task.reminder = resTask.reminder;
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
			return data;
		},
		async fetchTask(id) {
			const res = await fetch(`/api/tasks/${id}`);
			const data = await res.json();
			return data;
		}
	},
    async created() {
        this.tasks = await this.fetchTasks();
    },
}
</script>