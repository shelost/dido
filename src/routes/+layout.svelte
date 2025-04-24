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

<div class = 'mobile'>
	<a href = 'https://www.ahnheewon.com'>
		<img src = 'ahnheewon3.png' alt = 'Dido' />
	</a>
	<h1> This site is best viewed on desktop! </h1>
	<p> Thanks for your understanding! </p>

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

	.mobile{
		display: none;
	}

	@media (max-width: 800px) {
		.mobile{
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			height: 100vh;
			width: 100vw;
			background: #fbfcff;
			position: fixed;
			top: 0;
			left: 0;
			z-index: 100;			transition: .2s ease;

			text-align: center;
			img{
				height: 32px;
				margin-bottom: 40px;
			}
			h1{
				font-size: 24px;
				font-weight: 600;
				letter-spacing: -0.5px;
				line-height: 1.2;
				margin-bottom: 8px;
				width: 90%;
			}
			p{
				font-size: 16px;
				font-weight: 400;
				letter-spacing: -0.32px;
				width: 90%;
			}

		}
	}
</style>
