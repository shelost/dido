<script>
	import Navbar from '../Navbar.svelte';
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class = 'page'>

	<div class = 'splash'>
		<h2> Welcome Back, Heewon! </h2>
		<p>
			Here's what's new with your account.
		</p>
	</div>

	<div class = 'content'>
		<h2> Hey Heewon — Welcome Back! </h2>
	</div>

</div>


<style lang="scss">

	.splash{
		margin: 80px 0;
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 8px;

		h2{
			font-family: 'Inter', sans-serif;
			font-size: 48px;
			font-weight: 600;
			letter-spacing: -1.5px;
		}

		p{
			font-family: 'Inter', sans-serif;
			font-size: 18px;
			font-weight: 400;
			letter-spacing: -.5px;
			color: #9295a7;
		}
	}
</style>



