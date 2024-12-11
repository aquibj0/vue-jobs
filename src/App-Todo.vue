<script setup>

import {onMounted, ref} from 'vue'

// export default {
// 	setup(props) {
// 		const name = ref('John Doe');
// 		const status = ref('active');
// 		const tasks = ref(['first Task', 'Second Task', 'Third Task']);

// 		const toggleStatus = () => {
// 			if (status.value === 'active') {
// 				status.value = 'pending';
// 			} else if (status.value === 'pending') {
// 				status.value = 'inactive';
// 			} else {
// 				status.value = 'active';
// 			}
// 		};

// 		return {
// 			name,
// 			status, 
// 			tasks,
// 			toggleStatus
// 		}

// 	}
// }

	const name = ref('John Doe');
	const status = ref('active');
	const tasks = ref(['first Task', 'Second Task', 'Third Task']);
	const newTask = ref('')

	const toggleStatus = () => {
		if (status.value === 'active') {
			status.value = 'pending';
		} else if (status.value === 'pending') {
			status.value = 'inactive';
		} else {
			status.value = 'active';
		}
	};

	const addTask = () => {

		if (newTask.value.trim() !== '') {
			tasks.value.push(newTask.value);
			newTask.value = '';
		}
	}

	const deleteTask = (index) => {
		tasks.value.splice(index, 1)
	}

/**
 * Load todos using fetch api 
 */
onMounted(async () => {
	try {
		const response = await fetch('https://jsonplaceholder.typicode.com/todos');
		const data = await response.json();
		tasks.value = data.map((task) => task.title);
		// console.log(tasks.value)
	} catch (error) {
		console.log('Error fetching data', `${error}`);
		
	}
});
</script>


<template>
	<h1>{{name}}</h1>
	<p v-if="status === 'active'">User is active</p>
	<p v-else-if="status === 'pending'">User is pending</p>
	<p v-else>User is inactive</p>


	<form @submit.prevent="addTask">
		<label for="newTask">Add Task</label>
		<input type="text" id="newTask" name="newTask" v-model="newTask">
		<button type="submit">Submit</button>
	</form>

	<h3>Tasks</h3>

	<ul>
		<li v-for="(task, index) in tasks" :key="task">
			<span>{{ task }}</span>
			<button @click="deleteTask(index)">x</button>
		</li>
	</ul>

	<button @click="toggleStatus">Change Status</button>
	
</template>

<style>
	/* h1{color: re;} */
</style>