<script>
    import { page } from '$app/stores';
    import { goto } from '$app/navigation';
    import { onMount } from 'svelte';

    let Nav = [
        {
            icon: 'Home',
            label: 'Home',
            href: '/'
        },
        {
            icon: 'Store',
            label: 'My Store',
            href: '/store'
        },
        {
            icon: 'Wallet',
            label: 'Income',
            href: '/income'
        },
        {
            icon: 'Chart',
            label: 'Analytics',
            href: '/analytics'
        },
        {
            icon: 'Person',
            label: 'Customers',
            href: '/customers'
        },
        {
            icon: 'People',
            label: 'Community',
            href: '/community'
        },
        {
            icon: 'Funnel',
            label: 'Funnels',
            href: '/funnels'
        },
        {
            icon: 'Smile',
            label: 'Referrals',
            href: '/referrals'
        },
    ];

    // Function to just position the pill without navigation
    function positionPill(index) {
        const navBtn = document.getElementById(`nav-btn-${index}`);
        const pill = document.getElementById('active-pill');

        if (navBtn && pill) {
            const rect = navBtn.getBoundingClientRect();
            const navbarRect = document.getElementById('navbar').getBoundingClientRect();

            // Position the pill relative to the navbar
            pill.style.top = `${rect.top - navbarRect.top}px`;
            pill.style.left = `${rect.left - navbarRect.left}px`;
            pill.style.height = `${rect.height}px`;
            pill.style.width = `${rect.width}px`;
            pill.style.opacity = '1';
        }
    }

    // Function to handle click - positions the pill AND navigates
    function handleNavClick(index) {
        positionPill(index);
        // Navigate to the page
        goto('/demo' + Nav[index].href);
    }

    // Handle window resize to reposition the pill without navigation
    function updateActivePillPosition() {
        // Find which nav button is active based on the current URL
        const activeIndex = Nav.findIndex(n => {
            if (n.href === '/') {
                return $page.url.pathname === '/demo';
            }
            return $page.url.pathname.includes(n.href);
        });

        if (activeIndex >= 0) {
            positionPill(activeIndex);
        }
    }

    onMount(() => {
        // Initial positioning of the pill
        updateActivePillPosition();

        // Update pill position on window resize
        window.addEventListener('resize', updateActivePillPosition);

        return () => {
            window.removeEventListener('resize', updateActivePillPosition);
        };
    });
</script>

<div id='navbar'>
    <div id='active-pill'></div>

    <img id = 'logo'src = '/logo-text.svg' alt = 'Logo' />

    {#each Nav as n, i}
        <div
            id={`nav-btn-${i}`}
            class='navbtn'
            class:active={n.href == '/' ? $page.url.pathname == '/demo' : $page.url.pathname.includes(n.href) }
            on:click={() => handleNavClick(i)}
        >
            <img src = '/stanicons/id={n.icon}.svg' class = 'icon'alt = 'Icon' />
            <h2>{n.label} </h2>
        </div>
    {/each}
</div>

<style lang="scss">

    #logo{
        height: 28px;
        margin: 0 12px 18px 12px;
    }

    #navbar{
        //background: rgb(232, 233, 255);
        position: sticky;
        flex-shrink: 0;
        top: 0;
        left: 0;
        width: 200px;
        height: calc(100% - 16px);
        padding: 24px 12px;
        border-radius: 12px;
        margin: 8px;
        box-sizing: border-box;
        position: relative;
    }

    #active-pill {
        position: absolute;
        left: 0;
        background: #6355FF;
        border-radius: 0 24px 24px 0;
        border-radius: 32px;
        box-shadow: -8px 12px 16px rgba(black, .2),
                    inset 1px 2px 3px rgba(white, .2),
                    inset -1px -3px 8px rgba(#030025, .15);
        transition: all 0.2s ease;
        z-index: 1;
        opacity: 0;
    }

    .navbtn{
        padding: 12px 12px 14px 18px;
        border-radius: 0 24px 24px 0;
        border-radius: 32px;
        transition: .3s ease;
        cursor: pointer;
        position: relative;
        z-index: 2;

        display: flex;
        align-items: center;
        gap: 8px;


        img{
            height: 22px;
            transition: .3s ease;
        }

        h2{
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 15px;
            font-weight: 600;
            letter-spacing: -.24px;
            transition: 0.3s ease;
        }

        &:hover{
            background: rgba(#6355FF, .1);
        }

        &.active{
            img{
                filter: invert(1) brightness(2) drop-shadow(0 4px 2px rgba(black, .3));
            }
            h2{
                color: white;
                text-shadow: -6px 6px 8px rgba(black, .3);
            }
        }
    }
</style>