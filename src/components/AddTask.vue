<template>
  	<form
		class="add-form"
		@submit="onSubmit"
	>
    <div class="form-control">
    	<label>Task</label>
    	<input
			v-model="text"
			type="text"
			name="text"
			placeholder="Add Task"
		/>
    </div>
    <div class="form-control">
      	<label>Day & Time</label>
      	<input
			v-model="day"
        	type="text"
			name="day"
        	placeholder="Add Day & Time"
      	/>
    </div>
    <div class="form-control form-control-check">
     	<label>Set Reminder</label>
      	<input
			type="checkbox"
			name="reminder"
			v-model="reminder"
		/>
    </div>
	
	<Button
		color="#2e772e"
		text="Save task"
		type="submit"
	/>
  </form>
</template>

<script>
	import Button from './Button'

	export default {
		name: 'AddTask',
		components: {
			Button,
		},
		data: () => ({
			text: '',
			day: '',
			reminder: false
		}),
		methods: {
			onSubmit(e) {
				e.preventDefault();

				if (!this.text) {
					alert("type your task")
					return ;
				}

				const newTask = {
					id: Math.floor(Math.random() * 100000),
					text: this.text,
					day: this.day,
					reminder: this.reminder
				};

				this.$emit('add-task', newTask);

				this.text = '';
				this.day = '';
				this.reminder = false;
			}
		}
	};
</script>

<style scoped>

form {
	margin: 0px 20px 0px 20px;
}

.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}

</style>