<script>
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';

	import theme from '$lib/store/theme';
	import FooterElement from '$components/bootstrap/FooterElement.svelte';
	import NavigationElement from '$components/bootstrap/NavigationElement.svelte';

	import '$lib/assets/css/app.css';
	import '$lib/assets/css/typing.css';

	const activeSearch = writable(false);
	setContext('activeSearch', activeSearch);
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="" />
	<link
		href="https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;700&family=Roboto:wght@300;400;500&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="{$theme} flex flex-col h-screen {$activeSearch && 'overflow-y-hidden'}">
	<div class="sticky top-0 z-50 bg-gray-light dark:bg-gray-dark">
		<NavigationElement />
	</div>
	<main class="bg-gray-light dark:bg-gray-dark flex-grow"><slot /></main>
	<FooterElement />
</div>
