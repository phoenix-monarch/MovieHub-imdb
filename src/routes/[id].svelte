<script context="module">
	import Movie from '$lib/service/Movie';
	// @type {import('@sveltejs/kit').Load}
	export async function load({ params }) {
		const pageId = params.id;
		const [movie, similar, credits, providers] = await Promise.allSettled([
			Movie.getDetail(pageId),
			Movie.getSimilar(pageId),
			Movie.getCredits(pageId),
			Movie.getProviders(pageId)
		]);

		return {
			maxage: 0,
			props: {
				movie: movie.value.ok && (await movie.value.json()),
				similar: similar.value.ok && (await similar.value.json()),
				credits: credits.value.ok && (await credits.value.json()),
				providers: providers.value.ok && (await providers.value.json())
			}
		};
	}
</script>

<script>
	import MovieSection from '$components/templates/MovieSection.svelte';
	import CastSection from '$components/templates/CastSection.svelte';
	import MovieDetailHero from '$components/elements/MovieDetailHero.svelte';

	export let movie, similar, credits, providers;
</script>

<svelte:head>
	<title>{movie.title}</title>
</svelte:head>

<div>
	<div class="bg-dark">
		<div class="sm:container">
			<MovieDetailHero {movie} {providers} />
		</div>
	</div>
	<div />
	<div class="container">
		<div class="mt-4">
			<CastSection collection={credits.cast} />
		</div>

		<h2 class="my-4 ">Similar Movies</h2>
		<MovieSection collection={similar} />
	</div>
</div>
