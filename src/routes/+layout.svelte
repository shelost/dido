<script>
	import Header from './Header.svelte';
	import Navbar from './Navbar.svelte';
	import '../app.css';

	let { children } = $props();
</script>


<svelte:head>
	<title> Dido </title>
	<meta name="description" content="A More Elegant UI Library" />
	<meta name="view-transition" content="same-origin" />
	<link rel="icon" href="/logo-square.png" />
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
</svelte:head>

<div class="app">
	<Header />
	<main>
		{@render children()}
	</main>

</div>


<style lang="scss">
	.app {
		display: flex;
		width: 100vw;
		min-height: 100vh;
		overflow-x: hidden;
		background: none;
		//gap: 40px;
	}

	main {
		flex: 1;
		//width: calc(100% - 240px);
		overflow-x: hidden;
		box-sizing: border-box;
		padding: 0 40px;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
