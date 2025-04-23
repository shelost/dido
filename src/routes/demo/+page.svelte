<script>
	import Navbar from '../Navbar.svelte';
	import { fly } from 'svelte/transition';
	import Chart from '$lib/components/Chart.svelte';
	import Cashout from '$lib/components/Cashout.svelte';
	import Table from '$lib/components/Table.svelte';
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class = 'page'>

	<div class = 'splash'>
		<div class = 'pfp' in:fly={{y: 50, delay: 100}}>
			<img src = '/rafaella.png' alt = 'pfp' />
		</div>
		<h2 in:fly={{y: 50, delay: 150}}> Welcome Back, Rafaella! </h2>
		<p in:fly={{y: 50, delay: 200}}>
			Here's what's new with your account.
		</p>
	</div>

	<div class = 'content'>
		<div class = 'row'>
			<div class = 'chart card'>
				<Chart />
			</div>
			<div class = 'cashout card'>
				<Cashout />
			</div>
		</div>
		<div class = 'table card'>
			<Table />
		</div>
	</div>

</div>


<style lang="scss">

	.row{
		display: flex;
		gap: 0px;
	}

	.chart{
		flex: 3;
		height: 240px;
	}

	.cashout{
		flex: 1;
	}

	.pfp{
		width: 160px;
		height: 160px;
		background: black;
		box-shadow: -6px 12px 24px rgba(black, 0.2);
		border-radius: 50%;
		overflow: hidden;

		img{
			width: 100%;
			height: 100%;
			object-fit: cover;
			margin-top: 20px;
		}
	}

	.splash{
		margin: 40px 0 80px 0;
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



