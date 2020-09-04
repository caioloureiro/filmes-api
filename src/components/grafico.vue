<template>

	<div>
		<pie-chart :data="chartData"></pie-chart>
	</div>
	
</template>

<script>
export default {
	name: 'grafico',
	
	data: function(){
		
		return{
			
			chartData: {
				
				'Nokia': 150,
				'Samsung': 120
				
			}
			
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
