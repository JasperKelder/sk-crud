<script lang="ts">
	import { enhance } from '$app/forms';
	import { fade } from 'svelte/transition';
	import { flip } from 'svelte/animate';
	import type { PageData } from './$types';

	export let data: PageData;

	$: ({ articles } = data);
</script>

<div class="grid">
	<div>
		<h2>Articles</h2>

		{#each articles as article (article.id)}
			<article
				in:fade={{ duration: 400 }}
				out:fade={{ duration: 300 }}
				animate:flip={{ duration: 600 }}
			>
				<header>{article.title}</header>
				<p>
					{article.content}
				</p>

				{#if article.userId === data.user?.userId}
					<form action="?/deleteArticle&id={article.id}" method="POST" use:enhance>
						<button type="submit" class="outline secondary">Delete Article</button>
					</form>
					<a href="/{article.id}" role="button" class="outline constrast" style="width: 100%;"
						>Edit Article</a
					>
				{/if}
			</article>
		{/each}
	</div>

	{#if data.user}
		<form action="?/createArticle" method="POST" use:enhance>
			<h3>New Article</h3>

			<label for="title">Title</label>
			<input type="text" id="title" name="title" />

			<label for="title">Content</label>
			<textarea id="content" name="content" rows={5} />

			<button type="submit">Add Article</button>
		</form>
	{/if}
</div>
