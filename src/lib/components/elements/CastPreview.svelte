<script>
	export let person;
</script>

<a href="/person/{person.id}" class="bg-light dark:bg-gray-dark dark:text-gray-light">
	<div class="overflow-hidden relative group rounded-lg sm:rounded-xl">
		<div class="absolute flex flex-col justify-end w-full h-full z-20 text-light">
			<div class="font-secondary text-center px-4 font-bold transition-all text-sm sm:text-base">
				{person.name}
			</div>
			<div class="font-secondary text-center pb-4 font-medium transition-all text-xs opacity-50">
				{person.character}
			</div>
		</div>
		<div
			class="bg-gradient-to-t from-dark to-transparent absolute z-10 w-full h-full hover:opacity-0"
		/>
		<div
			class="bg-gradient-to-tr from-primary to-primary-light absolute z-10 w-full h-full opacity-0 group-hover:opacity-50 transition-all duration-500 ease-out"
		/>
		<img
			class="object-cover object-center w-full h-36 sm:h-48 group-hover:scale-105 transition-all duration-200"
			src={person?.profile_path
				? `https://image.tmdb.org/t/p/w500${person.profile_path}`
				: '/img/mesh.png'}
			alt={person.name}
			on:error={(ev) => (ev.target.src = '/img/mesh.png')}
		/>
	</div>
</a>
