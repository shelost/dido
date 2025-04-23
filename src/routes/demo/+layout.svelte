<script>
    import Navbar from '../Navbar.svelte';
    import { page } from '$app/stores';
    import { fly } from 'svelte/transition';

    $: crumbs = $page.url.pathname.split('/').slice(2)

    $: crumbs.length == 0 ? crumbs.push('home') : null

    function titleCase(str){
        return str.replace(/\b\w/g, char => char.toUpperCase());
    }

</script>

<div id = 'app' in:fly={{y: 50, duration: 400}} out:fly={{y: 50, duration: 200}}>
	<Navbar />

	<div id = 'main'>
        <div id = 'titlebar'>
            <div class = 'crumbs'>
                {#each crumbs as crumb}
                    <h2> {titleCase(crumb)} </h2>
                {/each}
            </div>
            <div class = 'link'>
                <h2> stan.store/rafaella </h2>
            </div>
        </div>
        <div id = 'page'>
            <slot />
        </div>
	</div>
</div>

<style lang="scss">

    $dark: #0d1852;

:global(number-flow-svelte) {
	--number-flow-char-height: 0.85em;
	font-size: 52px;
	letter-spacing: -2.5px;
	font-weight: 700;
	font-family: 'Inter', sans-serif;
	color: $dark;
}


	#app{
		display: flex;
        justify-content: flex-start;
        align-items: flex-start;
		background: white;
        //background: rgba(238, 245, 255, .0);
        background-image: linear-gradient(to bottom, rgba(#6355FF, .05) 25%, rgba(#6355FF, .15));
		box-shadow: -12px 48px 72px rgba(#030025, .3);
		border-radius: 12px;
		border: 1px solid rgba(white, .2);
		overflow: hidden;
		margin: 0px;
        margin-top: 54px;

		height: calc(100vh - 84px);


        #titlebar{
            background: white;
            padding: 14px 14px;
            box-sizing: border-box;
            border-bottom: 1px solid rgba(black, .08);

            display: flex;
            justify-content: space-between;
            align-items: center;

            h2{
                color: #030025;
                font-family: 'Plus Jakarta Sans', sans-serif;
                font-size: 16px;
                font-weight: 600;
                letter-spacing: -.2px;
            }

            .crumbs{
                display: flex;
                gap: 8px;

            }

            .link{
                h2{
                    color: #6355FF;
                }
            }


        }

		#main{
			flex: 1;
            height: 100%;
            //height: calc(100% - 16px);
            //border-radius: 12px;
            overflow-y: scroll;
            padding: 0;
            box-sizing: border-box;
            gap: 0;

           // margin: 8px;
            background: white;
            box-shadow: 12px 18px 36px rgba(#030025, .2), inset -8px 8px 8px rgba(#030025, .02);

            #page{
                width: 100%;
                padding: 24px 36px;
                box-sizing: border-box;
            }
		}
	}
</style>
