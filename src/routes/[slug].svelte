<script context="module">
	export async function preload({ params, query }) {
		return {
			page: {
				slug: params.slug
			}
		};
	}
</script>

<svelte:head>
	<title>Joponlu</title>
</svelte:head>

<script>
	import CardManager from '../components/CardManager.svelte';
	import CardView from '../components/CardView.svelte';

	export let page;
</script>

<main>
	<h1>{page.slug}</h1>
	<CardManager>
		<CardView x={100} y={100} width={300} title="Welcome to my site">
			<h2>Hello World</h2>
			<p>Lorem ipsum dolor sit amet, <a href="//google.com">consectetur adipisicing</a> elit. Esse, nesciunt velit! Corrupti voluptatum voluptatem fuga excepturi, tenetur, eum expedita sit quisquam eligendi, culpa sed officia perspiciatis laudantium magni. Explicabo, dignissimos!</p>
		</CardView>
		<CardView x={200} y={200} width={300} title="Welcome to my site">
			<h2>Hello World</h2>
			<p>Lorem ipsum dolor sit amet, <a href="//google.com">consectetur adipisicing</a> elit. Esse, nesciunt velit! Corrupti voluptatum voluptatem fuga excepturi, tenetur, eum expedita sit quisquam eligendi, culpa sed officia perspiciatis laudantium magni. Explicabo, dignissimos!</p>
		</CardView>
		<CardView x={300} y={300} width={300} title="Welcome to my site">
			<h2>Hello World</h2>
			<p>Lorem ipsum dolor sit amet, <a href="//google.com">consectetur adipisicing</a> elit. Esse, nesciunt velit! Corrupti voluptatum voluptatem fuga excepturi, tenetur, eum expedita sit quisquam eligendi, culpa sed officia perspiciatis laudantium magni. Explicabo, dignissimos!</p>
		</CardView>
	</CardManager>
</main>

<style>
	[contenteditable=true]:focus {
		border: 4px dashed black;
	}

	h1 {
		color: white;
	}

	:global(*) {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }

	:global(body) {
		background-image: url(../assets/back.png);
        cursor: url(../assets/cursor.png) 0 0, pointer;
	}

	:global(a) {
        cursor: url(../assets/cursor-fer.png) 10 10, pointer;
    }
</style>