<template>
	<div id="app">
		<h1>Tarefas</h1>
		<TaskGrid :tasks="tasks"></TaskGrid>
	</div>
</template>

<script>

import TaskGrid from './components/TaskGrid.vue'

export default {
	components:{ TaskGrid },
	data(){
		return{
			tasks:[
				{ name:'Pagar boletos', peding:false },
				{ name:'Estudar', peding:true },
			]
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
