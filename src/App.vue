<template>
	<div id="app">

		<h1>Filmes API em vue.js</h1>
		
		<div class="col50">

			<h2>TOP 100 DO ANO</h2>

			<form @submit.prevent="pesquisar">

				Digite o Ano: <input type="text" id="populares" v-model="inputFilme.ano"/>

				<button>Pesquisar</button>

			</form>

		</div>
		
		<div class="col50">

			<h2>Gêneros mais pontuados</h2>

			<column-chart :data="chartData" ></column-chart>
			
			<button @click="atualizarGrafico">Atualizar Gráfico</button>

		</div>
		
		<div class="separador"></div>

		<div class="col100">

			<div class="cardFilme" v-for="filme of filmes" :key="filme.id">

				<div class="capaFilme" v-bind:style="{ 'background-image': 'url(https://image.tmdb.org/t/p/w220_and_h330_face' + filme.poster_path + ')' }" >

					<div class="capaFilmeEscurecer">

						<a href="#" target="_blank"></a>

					</div>

				</div>

				<div class="filmeTitulo">{{ filme.title }}</div>
				<div class="filmeTitulo">Nota: {{ filme.vote_average }}</div>

			</div>

		</div>

	</div>
</template>

<script>

//https://api.themoviedb.org/3/movie/top_rated?api_key=486bec8dc29c47e695e212b372641f82&primary_release_year=2020&page=1
//https://api.themoviedb.org/3/genre/movie/list?api_key=486bec8dc29c47e695e212b372641f82&language=pt

import axios from 'axios'

const api_key = '486bec8dc29c47e695e212b372641f82'

export default {
	
	components:{},
	
	data(){
		
		return{
			
			inputFilme: {
				ano: ''
			},
			filmes01: [],
			filmes02: [],
			filmes03: [],
			filmes04: [],
			filmes05: [],
			filmesBOX: [],
			filmes: [],
			generos: [],
			chartData: [
			
				[ 'Ação' , 0 ],
				[ 'Aventura' , 0 ],
				[ 'Animação' , 0 ],
				[ 'Comédia' , 0 ],
				[ 'Crime' , 0 ],
				[ 'Documentário' , 0 ],
				[ 'Drama' , 0 ],
				[ 'Família' , 0 ],
				[ 'Fantasia' , 0 ],
				[ 'História' , 0 ],
				[ 'Terror' , 0 ],
				[ 'Música' , 0 ],
				[ 'Mistério' , 0 ],
				[ 'Romance' , 0 ],
				[ 'Ficção científica' , 0 ],
				[ 'Cinema TV' , 0 ],
				[ 'Thriller' , 0 ],
				[ 'Guerra' , 0 ],
				[ 'Faroeste' , 0 ],
			
			],
			novoChartData: [],
			
		}
		
	},
	
	methods:{
		
		listar(){
			
			let one = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=1'
			let two = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=2'
			let three = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=3'
			let four = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=4'
			let five = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=5'
			
			const requestOne = axios.get(one);
			const requestTwo = axios.get(two);
			const requestThree = axios.get(three);
			const requestFour = axios.get(four);
			const requestFive = axios.get(five);
			
			axios.all( [
				requestOne,
				requestTwo,
				requestThree,
				requestFour,
				requestFive
			] ).then( axios.spread( ( ...responses ) => {
				
				const responseOne = responses[0].data.results
				const responseTwo = responses[1].data.results
				const responesThree = responses[2].data.results
				const responesFour = responses[3].data.results
				const responesFive = responses[4].data.results
				
				this.filmes01 = responseOne,
				this.filmes02 = responseTwo,
				this.filmes03 = responesThree,
				this.filmes04 = responesFour,
				this.filmes05 = responesFive,
				
				this.filmesBOX = this.filmes01.concat(this.filmes02, this.filmes03, this.filmes04, this.filmes05),
				
				this.filmes = this.filmesBOX
				
				//console.log('this.filmes:')
				//console.log(this.filmes)
				
				let filme;
				
				for( filme of this.filmes ){
					
					//console.log( 'filme.genre_ids[0]: '+ filme.genre_ids[0] )
					
					if( filme.genre_ids[0] == 28 ){ this.chartData[0][1]++ }
					if( filme.genre_ids[0] == 12 ){ this.chartData[1][1]++ }
					if( filme.genre_ids[0] == 16 ){ this.chartData[2][1]++ }
					if( filme.genre_ids[0] == 35 ){ this.chartData[3][1]++ }
					if( filme.genre_ids[0] == 80 ){ this.chartData[4][1]++ }
					if( filme.genre_ids[0] == 99 ){ this.chartData[5][1]++ }
					if( filme.genre_ids[0] == 18 ){ this.chartData[6][1]++ }
					if( filme.genre_ids[0] == 10751 ){ this.chartData[7][1]++ }
					if( filme.genre_ids[0] == 14 ){ this.chartData[8][1]++ }
					if( filme.genre_ids[0] == 36 ){ this.chartData[9][1]++ }
					if( filme.genre_ids[0] == 27 ){ this.chartData[10][1]++ }
					if( filme.genre_ids[0] == 10402 ){ this.chartData[11][1]++ }
					if( filme.genre_ids[0] == 9648 ){ this.chartData[12][1]++ }
					if( filme.genre_ids[0] == 10749 ){ this.chartData[13][1]++ }
					if( filme.genre_ids[0] == 878 ){ this.chartData[14][1]++ }
					if( filme.genre_ids[0] == 10770 ){ this.chartData[15][1]++ }
					if( filme.genre_ids[0] == 53 ){ this.chartData[16][1]++ }
					if( filme.genre_ids[0] == 10752 ){ this.chartData[17][1]++ }
					if( filme.genre_ids[0] == 37 ){ this.chartData[18][1]++ }
					
				}
				
				//console.log( 'this.chartData atualizado:' )
				//console.log( this.chartData )
				
				this.novoChartData = this.chartData
				
				//console.log( 'this.novoChartData:' )
				//console.log( this.novoChartData )
				
			} ) )
			
		},
		
		criarArrayGenero(){
		
			let generos = 'https://api.themoviedb.org/3/genre/movie/list?api_key='+ api_key +'&language=pt'
			
			let requestGenero = axios.get( generos )
			
			axios.all( [ requestGenero ] ).then( axios.spread( ( ...responses ) => {
				
				let responseGeneros = responses[0].data.genres;
				
				this.generos = responseGeneros
				
				//console.log('this.generos:')
				//console.log(this.generos)
				
			} ) )
		
		},
		
		pesquisar(){
			
			if(document.getElementById('populares').value != ''){
				
				this.listar()
				this.criarArrayGenero()
				//this.inputFilme = {}
				
			}else{
				
				alert('Digite um valor válido.');
				
			}
		
		},
		
		atualizarGrafico(){
		
			//alert('ok')
			//this.chartData = this.novoChartData
			
			//console.log( 'this.novoChartData[0]' );
			//console.log( this.novoChartData[0][0] );
			
			this.chartData = [
			
				[ this.novoChartData[0][0] , this.novoChartData[0][1] ],
				[ this.novoChartData[1][0] , this.novoChartData[1][1] ],
				[ this.novoChartData[2][0] , this.novoChartData[2][1] ],
				[ this.novoChartData[3][0] , this.novoChartData[3][1] ],
				[ this.novoChartData[4][0] , this.novoChartData[4][1] ],
				[ this.novoChartData[5][0] , this.novoChartData[5][1] ],
				[ this.novoChartData[6][0] , this.novoChartData[6][1] ],
				[ this.novoChartData[7][0] , this.novoChartData[7][1] ],
				[ this.novoChartData[8][0] , this.novoChartData[8][1] ],
				[ this.novoChartData[9][0] , this.novoChartData[9][1] ],
				[ this.novoChartData[10][0] , this.novoChartData[10][1] ],
				[ this.novoChartData[11][0] , this.novoChartData[11][1] ],
				[ this.novoChartData[12][0] , this.novoChartData[12][1] ],
				[ this.novoChartData[13][0] , this.novoChartData[13][1] ],
				[ this.novoChartData[14][0] , this.novoChartData[14][1] ],
				[ this.novoChartData[15][0] , this.novoChartData[15][1] ],
				[ this.novoChartData[16][0] , this.novoChartData[16][1] ],
				[ this.novoChartData[17][0] , this.novoChartData[17][1] ],
				[ this.novoChartData[18][0] , this.novoChartData[18][1] ]
			
			]
			
			//console.log( 'this.chartData atualizado:' )
			//console.log( this.chartData )
		
		},
		
	}
	
}

</script>

<style>
	@import './assets/css/estilo.css';
</style>