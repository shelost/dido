<script>
	import Phone from '$lib/components/Phone.svelte'
	import { onMount } from 'svelte';
	import Sortable from 'sortablejs';
	import { writable } from 'svelte/store';
    import { fly, scale } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
    import { crossfade } from 'svelte/transition';
    import Tabs from '$lib/components/Tabs.svelte';

    // Tabs configuration
    let activeTab = 'products';
    const storeTabs = ['products', 'collections', 'settings'];
    const storeTabLabels = {
        products: 'My Store',
        collections: 'Landing Pages',
        settings: 'Design'
    };

    // Create a writable store for better reactivity
    const rowsStore = writable([
		{
			id: 1,
		    name: 'Join My Membership',
			type: 'Membership',
			price: 29.00,
		    img: 'vector/membership',
            thumbImg: 'vector/thumbnails/membership',
            visible: false
		},
		{
			id: 2,
			name: 'Digital Starter Kit',
			type: 'Digital Product',
			price: 49.00,
		    img: 'vector/digital-kit',
            thumbImg: 'vector/thumbnails/digital-kit',
            visible: false
		},
		{
			id: 3,
			name: '1:1 Coaching Call',
			type: 'Service',
			price: 99.00,
		    img: 'vector/coaching',
            thumbImg: 'vector/thumbnails/coaching',
            visible: false
		},
		{
			id: 4,
			name: 'Online Course Bundle',
			type: 'Digital Product',
			price: 149.00,
		    img: 'vector/course',
            thumbImg: 'vector/thumbnails/course',
            visible: false
		},
        {
			id: 5,
			name: 'Ultimate Ebook Guide',
			type: 'Digital Product',
			price: 19.99,
		    img: 'vector/ebook',
            thumbImg: 'vector/thumbnails/ebook',
            visible: false
		},
		{
			id: 6,
			name: 'Workshop Series',
			type: 'Live Event',
			price: 79.00,
		    img: 'vector/workshop',
            thumbImg: 'vector/thumbnails/workshop',
            visible: false
		},
	]);

	// Subscribe to the store to get the current value
	let Rows;
	const unsubscribe = rowsStore.subscribe(value => {
		Rows = value;
	});

	let cardsContainer;
	let sortableInstance;
    let animationsReady = false;

    // Function to handle image loading errors
    function handleImageError(event) {
        // If thumbnail fails, fall back to original image
        const img = event.target;
        const originalSrc = img.src.replace('/thumbnails/', '/');
        img.src = originalSrc;
    }

	onMount(() => {
        // Start showing the cards with a staggered animation
        const staggerDelay = 100; // Milliseconds between each card animation
        const animationDuration = 400; // Total animation duration per card

        // Small delay before starting animations to ensure DOM is fully rendered
        setTimeout(() => {
            animationsReady = true;

            // Mark all cards as visible at once - the staggering happens in the transition
            rowsStore.update(items => {
                return items.map(item => ({
                    ...item,
                    visible: true
                }));
            });

            // Initialize Sortable after all animations are complete
            const totalAnimationTime = (Rows.length * staggerDelay) + animationDuration + 100;

            setTimeout(() => {
                if (cardsContainer) {
                    sortableInstance = new Sortable(cardsContainer, {
                        animation: 150,
                        ghostClass: 'ghost-card',
                        handle: '.handle',
                        onEnd: (evt) => {
                            // Update the rows store after sorting
                            if (evt.oldIndex !== evt.newIndex) {
                                rowsStore.update(currentRows => {
                                    const items = [...currentRows];
                                    const movedItem = items.splice(evt.oldIndex, 1)[0];
                                    items.splice(evt.newIndex, 0, movedItem);
                                    return items;
                                });
                            }
                        }
                    });
                }
            }, totalAnimationTime);
        }, 100);

		// Clean up when component is destroyed
		return () => {
			if (sortableInstance) {
				sortableInstance.destroy();
			}
			unsubscribe();
		};
	});

    // Custom transition that combines fly and scale with staggered delay
    function flyAndScale(node, { y = 60, duration = 400 }) {
        // Get the index of this card from its data-id attribute
        const index = parseInt(node.getAttribute('data-id')) - 1;
        const delay = index * 50; // 100ms stagger between each card

        return {
            duration,
            delay,
            css: (t) => {
                const eased = quintOut(t);
                // Starting from slightly below and smaller, then animating to normal position
                return `
                    transform: translateY(${(1-eased) * y}px) scale(${0.95 + (eased * 0.05)});
                    opacity: ${eased};
                `;
            }
        };
    }
</script>

<div class="page">

    <section>
        <div class = 'tabs'>
            <Tabs activeTab={activeTab} tabs={storeTabs} tabLabels={storeTabLabels} />
        </div>

        <div class = 'card profile'>
            <div class = 'content'>
                <div class = 'img'>
                    <img src = '/rafaella.png' alt = 'Heewon Ahn' />
                </div>
                <div class = 'expo'>
                    <h1> Rafaella Delacroix </h1>
                    <h2> @rafaella</h2>
                </div>
            </div>
        </div>
        <div class="cards" bind:this={cardsContainer}>
            {#each Rows as row, i (row.id)}
                {#if row.visible}
                    <div class="card" data-id={row.id} in:flyAndScale={{ y: 20, duration: 400 }}>
                        <div class="handle">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <line x1="8" y1="6" x2="16" y2="6"></line>
                                <line x1="8" y1="12" x2="16" y2="12"></line>
                                <line x1="8" y1="18" x2="16" y2="18"></line>
                            </svg>
                        </div>
                        <div class="content">
                            <div class = 'img'>
                                <img
                                    src = '/{row.thumbImg || row.img}.jpg'
                                    alt = {row.name}
                                    loading="lazy"
                                    width="52"
                                    height="52"
                                    on:error={handleImageError}
                                />
                            </div>
                            <div class = 'expo'>
                                <h2>{row.name}</h2>
                                <h3>{row.type}</h3>
                                <h4>${row.price}</h4>
                            </div>
                        </div>
                    </div>
                {/if}
            {/each}
        </div>
    </section>

    <div class="phone">
        <Phone />
    </div>
</div>

<style lang="scss">
    .page {
        width: 100%;
        display: flex;
        justify-content: flex-start;
        gap: 32px;
    }

    .tabs {
        position: relative;
        margin: 12px 0 24px 0;
        display: flex;
        justify-content: flex-start;
    }

    .phone{
        width: 300px;
        height: 600px;
       // border: 1px solid rgba(black, .1);
        box-shadow: 8px 16px 48px rgba(#000010, .6), inset 1px 2px 3px rgba(white, .15), inset -1px -3px 8px rgba(#030025, .1);
        border-radius: 32px;
        margin: 16px;
        padding: 0;
        position: relative;
        overflow: hidden;
    }

    .handle{
        width: 24px;
        height: 32px;
        border-radius: 6px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: rgba(0,0,0,0.5);
        cursor: grab;
        background: rgba(black, .05);
    }

    section{
        flex: 1;
    }

    .cards {
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        gap: 12px;
        padding: 16px;
    }

    .card {
        background-color: white;
        border-radius: 16px;
        //box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        padding: 16px;
        min-width: 200px;
        margin: 0;
        transition: 0.2s ease;

        display: flex;
        align-items: center;
        gap: 16px;

        .content{
            display: flex;
            align-items: center;
            gap: 16px;
            .img{
                width: 52px;
                height: 52px;
                overflow: hidden;
                background: rgba(black, .1);
                border-radius: 6px;
                display: flex;
                align-items: center;
                justify-content: center;
                img{
                    width: 100%;
                    height: 100%;
                    object-fit: cover;
                }
            }
        }

        .expo{
            h2{
                font-size: 16px;
                font-weight: 500;
                letter-spacing: -0.36px;
                margin-bottom: 4px;
            }
            h3{
                font-size: 14px;
                font-weight: 400;
                letter-spacing: -0.16px;
                display: block;
                color: rgba(0,0,0,0.6);
                margin-bottom: 4px;
            }
            h4{
                font-size: 16px;
                font-weight: 450;
                letter-spacing: -0.32px;
                color: #6355FF;
            }
        }

        &:hover {
           // box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
           cursor: pointer;
            transform: translateY(-2px);
        }


        &.profile{
            margin: 0 12px 0px 12px;

            .img{
                width: 90px;
                height: 90px;
            }

            .expo{
                h1{
                    font-family: 'Inter', sans-serif;
                    font-size: 24px;
                    font-weight: 600;
                    letter-spacing: -.4px;
                    margin-bottom: 2px;
                }
                h2{
                    font-size: 16px;
                    font-weight: 400;
                    letter-spacing: -0.32px;
                }
            }

        }
    }

    .ghost-card {
        opacity: 0.5;
        background: #f0f0f0;
    }

    /* Apply slide-up animation to cards when they appear */
    @keyframes slideUp {
        from {
            opacity: 0;
            transform: translateY(30px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
</style>