<template>
	<div id="app">

		<h1>Filmes API em vue.js</h1>
		
		<div class="col25">
			<h2>100 MAIS POPULARES DO ANO</h2>
			<form @submit.prevent="pesquisar">
				Digite o Ano: <input type="text" id="populares" v-model="inputFilme.ano"/>
				<button>Pesquisar</button>
			</form>
		</div>
		
		<div class="col25">
			<h2>Gêneros mais pontuados</h2>
			<pie-chart :data="chartData"></pie-chart>
		</div>

		<div class="col100">
			<div class="cardFilme" v-for="filme of filmes" :key="filme.id">
				<div class="capaFilme" v-bind:style="{ 'background-image': 'url(https://image.tmdb.org/t/p/w220_and_h330_face' + filme.poster_path + ')' }" >
					<div class="capaFilmeEscurecer">
						<a href="#" target="_blank"></a>
					</div>
				</div>
				<div class="filmeTitulo">{{ filme.title }}</div>
			</div>
		</div>

	</div>
</template>

<script>

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
			chartData: {
				
				'Action': 10,
				'Adventure': 5,
				'Animation': 6,
				'Comedy': 4,
				'Crime': 6,
				'Documentary': 7,
				'Drama': 1,
				'Family': 10,
				'Fantasy': 5,
				'History': 4,
				'Horror': 1,
				'Music': 2,
				'Mystery': 5,
				'Romance': 3,
				'Science Fiction': 9,
				'TV Movie': 1,
				'Thriller': 1,
				'War': 3,
				'Western': 1
				
			}
			
		}
		
	},
	
	mounted(){
		
		//this.listar()
		
	},
	
	methods:{
		
		listar(){
			
			let one = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=1'
			let two = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=2'
			let three = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=3'
			let four = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=4'
			let five = 'https://api.themoviedb.org/3/movie/top_rated?api_key='+ api_key +'&primary_release_year='+ this.inputFilme.ano +'&page=5'
			
			const requestOne = axios.get(one)
			const requestTwo = axios.get(two)
			const requestThree = axios.get(three)
			const requestFour = axios.get(four)
			const requestFive = axios.get(five)
			
			axios.all([requestOne, requestTwo, requestThree, requestFour, requestFive]).then(axios.spread((...responses) => {
				
				const responseOne = responses[0].data.results;
				const responseTwo = responses[1].data.results;
				const responesThree = responses[2].data.results;
				const responesFour = responses[3].data.results;
				const responesFive = responses[4].data.results;
				
				this.filmes01 = responseOne,
				this.filmes02 = responseTwo,
				this.filmes03 = responesThree,
				this.filmes04 = responesFour,
				this.filmes05 = responesFive,
				
				this.filmesBOX = this.filmes01.concat(this.filmes02, this.filmes03, this.filmes04, this.filmes05),
				
				this.filmes = this.filmesBOX,
				
				console.log(this.filmes)
				
			}))
			
		},
		
		pesquisar(){
			
			if(document.getElementById('populares').value != ''){
				
				this.listar()
				//this.inputFilme = {}
				
			}else{
				
				alert('Digite um valor válido.');
				
			}
		
		}
		
	}
	
}

</script>

<style>
body{
margin:0;
margin-top:1vw;
margin-left:1vw;
margin-right:1vw;
padding:0;
/*
background-image:url("../img/template.png");
background-repeat:no-repeat;
background-position:center top;
background-size:100% auto;
font-family:'Segoe UI';
*/
background-color:rgb(243, 243, 243);
font-size:0.95vw;
line-height:1.7vw;
font-family:"Open Sans";
color:rgba(75,75,75,1);
}
a, a:visited, a:focus{
text-decoration:none;
font-weight:normal;
color:rgba(75,75,75,1);
font-size:0.95vw;
}
p{
text-align:justify;
}
select{
text-decoration:none;
font-weight:normal;
color:rgba(75,75,75,1);
font-size:0.95vw;
}
input{
width:100%;
height:100%;
padding:0vw;
border-top:0vw;
border-right:0vw;
border-left:0vw;
border-bottom:0.1vw solid rgba(0,0,0,0.3);
font-size:0.95vw;
line-height:3vw;
font-family:"Open Sans";
color:rgba(75,75,75,1);
background-color:rgba(240,240,240,0);
margin-top:0vw;
margin-bottom:1.5vw;
}
button{
width:100%;
height:100%;
background-color:rgba(0, 112, 107,1);
border:0.1vw solid rgba(0, 83, 73,1);
border-radius:0.5vw;
font-size:1.2vw;
line-height:4vw;
font-family:"Open Sans";
color:white;
cursor:pointer;
transition:all 0.3s ease-in-out;
}
button:hover{
background-color:rgba(100, 192, 171,1);
border:0.1vw solid rgba(70, 162, 141,1);
transition:all 0.3s ease-in-out;
}

/*Start - BLOCOS*/

.col100{
width:100%;
float:left;
}
.col25{
width:23%;
float:left;
padding:1%;
}

/*End - BLOCOS*/

/*Start - Card Filme*/

@keyframes marquee {
from{text-indent:0%}
to{text-indent:-200%}
}
.cardFilme{
margin-top:0.5vw;
margin-right:1vw;
margin-bottom:0.5vw;
width:11.6vw;
height:20vw;
float:left;
box-shadow:0vw 0.1vw 0.223vw rgba(0,0,0,0.1);
border-top-left-radius:0.223vw;
border-top-right-radius:0.223vw;
overflow:hidden;
cursor:pointer;
transition:all 0.1s linear;
background-color:rgb(250, 250, 250);
}
.cardFilme:hover{
/*transform:scale(1.2);*/
transition:all 0.1s linear;
}
.capaFilme{
width:100%;
height:18.5vw;
background-position:center center;
background-repeat:no-repeat;
opacity:1;
background-size:cover;
transition:all 0.3s ease;
}
.capaFilmeEscurecer{
width:100%;
height:100%;
background:rgba(0,0,0,0.3);
opacity:0;
transition:all 0.3s ease;
}
.capaFilme:hover{
background-position:center center;
background-size:cover;
transition:all 0.3s ease;
}
.capaFilme:hover .capaFilmeEscurecer, .capaFilme:hover{
opacity:1;
transition:all 0.3s ease;
}
.filmeTitulo{
width:86%;
height:1.5vw;
font-size:1vw;
padding-left:0.744vw;
padding-right:0.744vw;
line-height:1.5vw;
overflow:hidden;
font-weight:normal;
}
.filmeTitulo:hover{
animation:marquee 5s linear infinite;
}

/*End - Card Filme*/

</style>