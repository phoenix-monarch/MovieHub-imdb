<script>
	import { Icon, Clock, Link, Film, CurrencyDollar } from 'svelte-hero-icons';

	import Rating from '$components/elements/Rating.svelte';
	import ProviderSection from '$components/templates/ProviderSection.svelte';
	import { isEmpty } from '$lib/helper';
	export let movie, providers;

	const getYear = (date) => {
		const d = new Date(date);
		return d.getFullYear();
	};
</script>

<div class="sm:flex items-top sm:space-x-4 z-20 bg-dark py-6 px-2 sm:px-0 text-white">
	<img
		class="h-48 sm:h-56 mt-1"
		src="https://image.tmdb.org/t/p/w300{movie.poster_path}"
		alt="poster"
		on:error={(ev) => (ev.target.src = '/img/mesh.png')}
	/>
	<div class="flex flex-col dark:text-light">
		<div class="text-sm mt-4 sm:mt-0">{movie.tagline}</div>
		<div class="text-4xl font-secondary font-bold">
			{movie.title}
		</div>
		<div
			class="text-xs flex items-center justify-between sm:justify-start space-x-6 mt-2 text-gray"
		>
			{#if movie.genres}
				<div class="flex space-x-1 items-center">
					{#each movie.genres as genre, index}
						<div>{genre.name}</div>
						{#if movie.genres.length - 1 !== index}
							<div>|</div>
						{/if}
					{/each}
				</div>
			{/if}
			{#if movie.vote_average}
				<Rating value={movie.vote_average} />
			{/if}
		</div>
		<div class="text-xs flex items-center space-x-1 text-gray font-medium">
			{#if movie.release_date}
				<div>{getYear(movie.release_date)}</div>
			{/if}
			{#if movie.runtime}
				<div class="flex items-center ">
					<Icon src={Clock} class="w-3" />
					<span>{movie.runtime}</span>
				</div>
			{/if}
		</div>
		<div class="max-w-2xl">
			<p class="mt-2">{movie.overview}</p>
		</div>
		<div class="flex items-center space-x-4 text-xs text-gray mt-2">
			{#if movie.homepage}
				<div class="flex items-center space-x-1">
					<Icon src={Link} class="w-3" />
					<a rel="external" href={movie.homepage} target="_blank">Homepage</a>
				</div>
			{/if}
		</div>
		<ProviderSection collection={providers} />
	</div>
</div>
