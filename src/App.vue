<template>
	<div id="app">
		<h1>Tarefas</h1>
		<TaskProgress :progress="progress"/>
		<NewTask @taskAdded="addTask"></NewTask>
		<TaskGrid :tasks="tasks" @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState"></TaskGrid>
		<Footer/>
	</div>
</template>

<script>

import Footer from './components/Footer.vue'
import TaskProgress from './components/TaskProgress.vue'
import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTask.vue'

export default {
	components:{ TaskGrid, NewTask, TaskProgress,Footer },
	data(){
		return{
			tasks:[]
			}	
		},
		computed:{
			progress(){
				const total = this.tasks.length
				const done = this.tasks.filter( t => !t.pending).length
				return Math.round(done / total * 100) || 0
			}
		},
		watch:{
			tasks:{
				//"vigia" profundamente todos os objetos relacionados do array com deep
				deep: true,
				handler(){
					localStorage.setItem('tasks',JSON.stringify(this.tasks))
				}
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
			},
			deleteTask(i){
				this.tasks.splice(i,1)
			},
			toggleTaskState(i){
				this.tasks[i].pending = !this.tasks[i].pending
			}
		},
		created(){
				const json = localStorage.getItem('tasks')
				const array = JSON.parse(json)
				this.tasks =  Array.isArray(array) ? array : []
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
