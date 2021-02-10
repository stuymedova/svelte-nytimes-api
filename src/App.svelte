<script>
	import { onMount } from 'svelte';

	let articles = [];
	let results = [];

	onMount(async () => {
		const res = await fetch(`https://api.nytimes.com/svc/topstories/v2/home.json?api-key=`);
		articles = await res.json();
		// (line below) added due to the structure of an api
		results = articles.results;
	});
</script>

<main>
  <h1>NYT Top Stories</h1>
  <ul>
		{#each results as article}
			<li>
				<a href={article.short_url}><h2>{article.title}</h2></a>
				<p>{article.byline}</p>
				<p>{article.abstract}</p>
			</li>
		{:else}
			<p>loading...</p>
		{/each}
	</ul>
</main>