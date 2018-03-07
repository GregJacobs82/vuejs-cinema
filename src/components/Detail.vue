<template>
	<div id="detail" v-if="movie">
		<movie-item v-bind:movie="movie" v-bind:sessions="[]">
			<div class="movie-details">
				<p class="movie-genre">
					{{ movie.Genre }}
				</p>
			</div>
		</movie-item>
	</div>
</template>
<script>
	import MovieItem from './MovieItem.vue';
	export default {
		props: [
			'movies'
		],
		computed: {
			movie() {
				let movie = this.movies.find(movie => movie.id === this.$route.params.id);
				return movie ? movie.movie : null;
			}
		},
		components: {
			MovieItem
		}
	}
</script>
