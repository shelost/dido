<script>
	import { onMount, afterUpdate } from 'svelte';

	export let activeTab = 'home'; // Export activeTab prop for controlling active state externally
	export let tabs = ['home', 'about', 'demo']; // Allow custom tabs to be passed in
	export let tabLabels = { home: 'Home', about: 'About', demo: 'Demo' }; // Custom labels for tabs

	let Pill;
	let tabsContainer;
	let tabElements = {};

	function switchTab(tabId) {
		// Update the active tab
		activeTab = tabId;

		// Position the pill behind the tab immediately
		positionPillBehindTab(tabId);
	}

	function positionPillBehindTab(tabId) {
		// Get the tab element
		const tab = document.getElementById(tabId);
		if (!tab || !Pill || !tabsContainer) return;

		// Get the positions
		const tabRect = tab.getBoundingClientRect();
		const containerRect = tabsContainer.getBoundingClientRect();

		// Set the pill position relative to the tabs container
		Pill.style.left = `${tabRect.left - containerRect.left}px`;
		Pill.style.top = `${tabRect.top - containerRect.top}px`;
		Pill.style.width = `${tabRect.width}px`;
		Pill.style.height = `${tabRect.height}px`;
		Pill.style.opacity = '1';
	}

	// Update pill position when things change
	function updatePillPosition() {
		if (activeTab) {
			positionPillBehindTab(activeTab);
		}
	}

	// Create an observer to watch for layout changes
	function setupResizeObserver() {
		if (typeof ResizeObserver !== 'undefined') {
			const resizeObserver = new ResizeObserver(() => {
				updatePillPosition();
			});

			if (tabsContainer) {
				resizeObserver.observe(tabsContainer);
			}

			return () => {
				if (tabsContainer) resizeObserver.unobserve(tabsContainer);
				resizeObserver.disconnect();
			};
		}
		return () => {};
	}

	onMount(() => {
		// Initialize the pill position
		updatePillPosition();

		// Set up resize observer
		const cleanupResizeObserver = setupResizeObserver();

		// Add scroll and resize event listeners
		window.addEventListener('resize', updatePillPosition);
		window.addEventListener('scroll', updatePillPosition, true); // Capture phase to catch all scroll events

		return () => {
			// Clean up event listeners
			window.removeEventListener('resize', updatePillPosition);
			window.removeEventListener('scroll', updatePillPosition, true);
			cleanupResizeObserver();
		};
	});

	// Update after Svelte renders
	afterUpdate(() => {
		updatePillPosition();
	});
</script>

<div class="tabs" bind:this={tabsContainer}>
	<nav>
		<div id="pill" bind:this={Pill}></div>

		{#each tabs as tabId}
			<div
				id={tabId}
				class="tab"
				class:active={activeTab === tabId}
				on:click={() => switchTab(tabId)}
				bind:this={tabElements[tabId]}
			>
				<h2>{tabLabels[tabId] || tabId}</h2>
			</div>
		{/each}
	</nav>
</div>

<style lang="scss">
	.tabs {
		position: relative;
		display: inline-block;
		width: auto;
	}

	#pill {
		position: absolute;
		width: 40px;
		height: 40px;
		border-radius: 50px;
		background: rgba(#6355FF, 0.1);
        //border: 1px solid rgba(#6355FF, 0.2);
		//box-shadow: -2px 4px 10px rgba(#030025, 0.5), inset -2px -4px 8px rgba(#030025, 0.25), inset 2px 4px 8px rgba(white, 0.2);
		transition: .2s ease;
		z-index: 1;
		opacity: 0;
		pointer-events: none; /* Make sure pill doesn't interfere with clicks */
	}

	nav {
		display: flex;
		justify-content: center;
		position: relative;
		padding: 6px 6px;
		gap: 0px;
		z-index: 2;
	}

	.tab {
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		z-index: 3;
		padding: 10px 16px;
		border-radius: 50px;
		transition: .2s ease;

		h2 {
            font-family: 'Plus Jakarta Sans', sans-serif;
			font-size: 15px;
			font-weight: 600;
			letter-spacing: -.15px;
            transition: .2s ease;
		}

		&.active {
			h2 {
				color: #6355ff;
				//text-shadow: -2px 4px 8px rgba(black, .5);
			}
		}

		&:hover {
			//background: rgba(#6355FF, 0.05);
            h2{
                color: #6355ff;
            }

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

	#logo {
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
