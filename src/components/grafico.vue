<template>

	<div>
		<column-chart :data="chartData"></column-chart>
	</div>
	
</template>

<script>
export default {
	name: 'grafico',
	
	data: function(){
		
		return{
			
			chartData: {}
			
		}
		
	},
	
	components:{}
}
</script>

<style scoped>
	p{
		color:red;
		border:1px solid red;
	}
</style>
