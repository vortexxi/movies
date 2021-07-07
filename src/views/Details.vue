<template>
	<div class="movie-detail">
		<div class="posterInfo">
			<img :src="movie.Poster" alt="Movie poster not available" class="featured-img" />
		</div>
		<div class="content">
			<h2>{{movie.Title}}</h2>
			<p><span class="movieData">Year: </span>{{ movie.Year }}</p>	
			<!--from: https://www.youtube.com/watch?v=UHewcsv6uJY-->
			<p><span class="movieData">Rated: </span>{{ movie.Rated }}</p>
			<p><span class="movieData">Released: </span>{{ movie.Released }}</p>
			<p><span class="movieData">Runtime: </span>{{ movie.Runtime }}</p>
			<p><span class="movieData">Genre: </span>{{ movie.Genre }}</p>
			<p><span class="movieData">Director: </span>{{ movie.Director }}</p>
			<p><span class="movieData">Writer: </span>{{ movie.Writer }}</p>
			<p><span class="movieData">Actors: </span>{{ movie.Actors }}</p>
			<p><span class="movieData">Plot: </span>{{ movie.Plot }}</p>
			<p><span class="movieData">Language: </span>{{ movie.Language }}</p>
			<p><span class="movieData">Country: </span>{{ movie.Country }}</p>
			<p><span class="movieData">Awards: </span>{{ movie.Awards }}</p>
		</div>

	</div>
</template>
<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
export default{
	setup () {
		const movie = ref({});
		const route = useRoute();
		onBeforeMount(() => {
		fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
			.then(response => response.json())
			.then(data => {
				movie.value = data;
			});
		});
		return {
			movie
		}
	}

	}//export
	</script>

	<style>
	@import url('https://fonts.googleapis.com/css2?family=Anton&family=Roboto+Mono:ital,wght@0,300;0,400;0,500;1,700&display=swap');
	.movie-detail{
		color:#FFF;
		font-family: 'Roboto Mono', monospace;
		padding:25px;
		display: flex;
		flex-flow: column;
	}
	.movieData{
		color:#B7AC44;
	}
	.posterInfo{
		justify-content: center;
		margin:auto;
	}
	.content{
		padding: 25px;
		margin:auto;
	}
	.content h2{
		margin-top: 15px;
		margin-bottom: 15px;
		margin-left: auto;
		margin-right: auto;
	}
	</style>