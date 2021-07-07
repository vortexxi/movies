	<template>
		<div class="home">
			<div class="contenedor">
				<div class="poster">
					<!-- <router-link to="/movie/tt0409591"> -->
					<!-- <img class="posterImg" src="media/movies.jpg" alt="Movies-poster"> -->
					<div class="posterDiv">
						<h1>All the information about your favorite movies</h1>
					</div>
						
				</div><!--poster-->
				<div class="textoPoster">
							<div class="instructions">
								<h3>Search by movie, director, actor, year, etc.</h3>	
							</div>
							
							<!--FORM-->
							<div class="textBox">
								<form @submit.prevent="searchMovie()">
									<input class="textInput" type="text" placeholder="Type a movie, director, actor..." v-model="search">
									<input class="searchButton" type="submit" value="Search">
								</form>
								<!--RESULTS-->
								<div class="movies-list">
									<div class="movie" v-for="movie in movies" :key="movie.imdbID">

										<router-link :to="'/movie/' + movie.imdbID" class="movie-link">
											<div class="product-image">
												<img :src="movie.Poster" alt="Movie poster not available" />
											</div>
											<div class="detail">	
												<h3>{{ movie.Title }}</h3>
												<p class="type">{{ movie.Type }}</p>
												<p class="year">{{ movie.Year }}</p>
											</div>
										</router-link>
									</div><!--movie-->
								</div><!--list-->
							</div><!--text box-->
							<!-- </router-link> -->
						</div><!--TEXTO POSTER-->
			</div><!--contenedor-->
		</div><!--home-->
	</template>
		<style>
		@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:ital,wght@0,300;0,400;0,500;1,700&display=swap');
		.poster{		
			height: 250px;
			background-image: url('../assets/movies-opacity.png');
			background-color: #000;
			background-attachment: fixed;
			background-position: center;
			background-repeat: no-repeat;
			background-size: cover;
			display: flex;
		}
		.posterImg{
			width: 100%;
			position: fixed;
			height: 250px;
			overflow: scroll;
		}
		.textoPoster{
			display: flex;
			flex-flow: column;
		}
		.instructions{
			display: block;
			margin: auto;
			margin-top: 25px;
			margin-left: auto;
			margin-right: auto;
		}
		.instructions h3{
			color:#B7AC44;
			display: block;
			font-family: 'Roboto Mono', monospace;
			font-weight: regular;
			padding: 10px;
		}
		.textBox{
			margin-top: 25px;
			margin-bottom: 25px;
			margin-left: auto;
			margin-right: auto;
			padding:10px;
			background-color: #232323;
			display: block;
		}
		.textInput{
			max-width: 300px;
			padding:5px;
			margin:5px;
		}
		.searchButton{
			min-width: 50px;
			padding:5px;
			margin:5px;
		}

		.posterDiv{
			justify-content: center;
			margin: auto;
			text-align: center;
		}
		.poster h1{
			color:#FFF;
			font-family: 'Roboto Mono', monospace;
			font-weight: lighter;
			font-size: 24px;
			text-transform: uppercase;
			max-width: 380px;
			padding: 5px;
			justify-content: center;
			text-align: center;
		}
		.detail, img{
			font-family: 'Roboto Mono', monospace;
		}
		.movie{
			background-color: #B7AC44;
			display: flex;
			margin-bottom: 25px;
			margin-left: auto;
			margin-right: auto;
			padding: 25px;
			justify-content: center;
			text-align: center;
			border-style: ridge;
			border-width: 2px;
			border-color: #FF4500;
		}

		</style>
		<script>
		import { ref } from 'vue';
		import env from '@/env.js';
		export default{
			setup(){
				//search query from form
				const search = ref("");
				const movies = ref([]);

				const searchMovie = () => {
					if(search.value != ""){
						//console.log('apikey: ' + env.apikey);
					//let thePath = `http://www.omdbapi.com/?i=tt3896198&apikey=86a9c848`;	
					fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
						.then(response => response.json())
						.then(data => {
							movies.value = data.Search;
							search.value = "";
						});
						console.log(search.value);
						console.log(movies.value);
					}
				}//searchMovie

				//return function
				return{
					search,
					movies,
					searchMovie
				}
			}//setup

		}
		</script>
		

