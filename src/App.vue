<template>
	<div id="app">
		<h1>Tarefas</h1>
		<NewTask @taskAdded="addTask"></NewTask>
		<TaskGrid :tasks="tasks"></TaskGrid>
	</div>
</template>

<script>

import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTask.vue'

export default {
	components:{ TaskGrid, NewTask },
	data(){
		return{
			tasks:[
				// { name:'Pagar boletos', pending:false },
				// { name:'Estudar', pending:true },
			]
		}	
		},
		methods: {
			addTask(task){
				//Verifica se está na lista
				const sameName = t => t.name === task.name
				const reallyNew = this.tasks.filter(sameName).length == 0 
				if(reallyNew){
					this.tasks.push({
						name:task.name,
						pending: task.pending || true
					})
				}
			}
		}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: rgb(50,153,98);
		background: linear-gradient(0deg, rgba(50,153,98,1) 0%, rgba(20,20,20,1) 100%);
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
