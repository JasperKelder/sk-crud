<script lang="ts">
	import '@picocss/pico';
	import PageTransition from '$lib/PageTransition.svelte';
	import { navigating } from '$app/stores';

	$: navigate = ($navigating?.from !== $navigating?.to).toString();
</script>

<svelte:head>
	<title>SvelteKit CRUD</title>
</svelte:head>

<PageTransition trigger={navigate}>
	<div class="container">
		<hgroup>
			<h1>
				<a href="/"> SvelteKit CRUD 🔥</a>
			</h1>

			<h2>Built with SvelteKit & Prisma.</h2>
		</hgroup>
		<slot />
	</div>
</PageTransition>
