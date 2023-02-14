<script lang="ts">
	import '@picocss/pico';
	import PageTransition from '$lib/PageTransition.svelte';
	import { navigating } from '$app/stores';
	import type { PageData } from './$types';

	export let data: PageData;

	$: navigate = ($navigating?.from !== $navigating?.to).toString();
</script>

<svelte:head>
	<title>SvelteKit CRUD</title>
</svelte:head>

<div class="container">
	<nav>
		<ul>
			<li>
				<strong>
					<a href="/">SvelteKit CRUD</a>
				</strong>
			</li>
		</ul>
		<ul>
			{#if !data.user}
				<li><a href="/register">Register</a></li>
				<li><a href="/login">Login</a></li>
			{:else}
				<li>
					<form method="POST">
						<button formaction="/logout" type="submit">Logout</button>
					</form>
				</li>
			{/if}
		</ul>
	</nav>

	<PageTransition trigger={navigate}>
		<slot />
	</PageTransition>
</div>

<style>
	nav {
		min-height: 7rem;
	}
</style>
