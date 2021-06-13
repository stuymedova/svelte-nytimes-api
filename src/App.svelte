<script>
	import { onMount } from 'svelte';

	let articles = [];
	let results = [];
	// ToDo: enter an API key [ https://developer.nytimes.com/get-started ]
	let apiKey = '';

	onMount(async () => {
		const res = await fetch('https://api.nytimes.com/svc/topstories/v2/home.json?api-key=' + apiKey);
		articles = await res.json();
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