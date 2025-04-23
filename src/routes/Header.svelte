<script>
	import { page } from '$app/state';
	import logo from '$lib/images/svelte-logo.svg';
	import github from '$lib/images/github.svg';
  import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	function switchPage(page) {

		let tab = document.getElementById(page);
		let rect = tab.getBoundingClientRect();

		let pill = document.getElementById('pill');
		pill.style.left = `${rect.left}px`;
		pill.style.top = `${rect.top}px`;
		pill.style.width = `${rect.width}px`;
		pill.style.height = `${rect.height}px`;

		console.log('yo')


		if (page === 'home') {
			goto('/')
		} else {
			goto('/' + page)
		}
	}

	onMount(() => {

		switchPage('home')

		setTimeout(() => {
			switchPage('home')
		}, 1000)
		/*

		window.onresize = () => {
			switch (page.url.pathname) {
				case '/':
					switchPage('home')
					break;
				default:
					switchPage(page.url.pathname.substring(1));
					break
			}
		}
			*/
	})



</script>

<header>
	<div class="corner">
		<img id = 'logo' src='/logo-square.png' alt="SvelteKit" />
	</div>

	<nav>

		<div id = 'pill'></div>

			<div id = 'home' class = 'tab' class:active={page.url.pathname === '/'} on:click={() => {switchPage('home')}}>
				<h2>
					Home
				</h2>

			</div>
			<div id = 'about' class = 'tab' class:active={page.url.pathname === '/about'} on:click={() => {switchPage('about')}}>
				<h2>
					About
				</h2>
			</div>
			<div id = 'demo' class = 'tab' class:active={page.url.pathname.includes('demo')} on:click={() => {switchPage('demo')}}>
				<h2>
					Demo
				</h2>
			</div>

	</nav>

	<div class="corner">
		<a href="https://github.com/shelost/dido">
			<img src={github} alt="GitHub" />
		</a>
	</div>
</header>

<style lang="scss">


	header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		z-index: 10;
		margin-top: 10px;
		padding: 0 12px;
		box-sizing: border-box;
	}


	#pill{
		position: fixed;
		width: 40px;
		height: 40px;
		top: -40px;
		left: 50%;
		border-radius: 50px;
		background: #6355FF;
		box-shadow: -2px 4px 10px rgba(#030025, 0.5), inset -2px -4px 8px rgba(#030025, 0.25), inset 2px 4px 8px rgba(white, 0.2);
		transition: .2s ease;
	}

	nav {
		display: flex;
		justify-content: center;
		position: relative;

		padding: 6px 6px;
		border-radius: 50px;
		background: white;
		box-shadow: -10px 10px 10px rgba(#030025, 0.2), inset -2px -2px 4px rgba(#030025, 0.1), inset 2px 4px 8px rgba(white, 0.2);
		gap: 0px;
		z-index: 2;
	}

	.tab{
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		z-index: 4;
		padding: 8px 14px;
		border-radius: 50px;
		transition: .2s ease;
		h2{
			font-size: 14px;
			font-weight: 600;
			letter-spacing: -.4px;
		}
		&.active{
			h2{
				color: white;
				text-shadow: -2px 4px 8px rgba(black, .5);
			}
		}
		&:hover{
			background: rgba(black, .1);
		}
	}


	.corner a {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.corner img {
		width: 36px;
		height: 36px;
	}

	#logo{
		width: 36px;
		height: 36px;
		border-radius: 8px;
		object-fit: contain;
		box-shadow: -6px 6px 12px rgba(#030025, 0.3), inset -4px -4px 10px rgba(black, 0.9);
	}



	svg {
		width: 2em;
		height: 3em;
		display: none;
	}

	path {
		//fill: var(--background);
	}



	li {
		position: relative;
		height: 100%;
	}

	li[aria-current='page'] {
	}

	li[aria-current='page']::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0px;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--color-theme-1);
		transition: .2s ease;
	}

	nav a {
		font-family: 'Inter', sans-serif;
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		font-weight: 600;
		font-size: 14px;
		letter-spacing: -0.25px;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
