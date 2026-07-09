<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import Navbar from '$lib/Navbar.svelte';
	import Footer from '$lib/Footer.svelte';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<div class="outer_container">
	<div class="inner_container">
		<Navbar />

		{@render children()}
	</div>

	<Footer />
</div>

<style>
	.outer_container {
		display: flex;
		flex-direction: column;
		min-height: 100dvh;
		width: 100dvw;
	}
	.inner_container {
		display: flex;
		flex-direction: row;
		flex: 1;
		width: 100dvw;
	}

	    @media (width <= 1300px) {
		.inner_container {
			flex-direction: column;
		}
    }
</style>
