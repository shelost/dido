<script>
    import Navbar from '../Navbar.svelte';
    import { page } from '$app/stores';
</script>

<div id = 'app'>
	<Navbar />

	<div id = 'main'>
        <div id = 'titlebar'>
            <h2> {$page.url.pathname} </h2>
        </div>
		<slot />
	</div>
</div>

<style lang="scss">


	#app{
		display: flex;
        justify-content: flex-start;
        align-items: flex-start;
		background: white;
        background: rgb(238, 245, 255);
        background-image: linear-gradient(to bottom, rgba(#6355FF, .05) 25%, rgba(#6355FF, .1));
		box-shadow: -12px 32px 60px rgba(#030025, .2);
		border-radius: 12px;
		border: 1px solid rgba(white, .2);
		overflow: hidden;
		margin: 32px;

		height: calc(100vh - 64px);

        #titlebar{
            background: rgba(#030025, .05);
            padding: 12px 16px;
            border-radius: 24px;
            h2{
                font-size: 14px;
                letter-spacing: -.4px;
            }
        }

		#main{
			flex: 1;
            height: 100%;
            //height: calc(100% - 16px);
            //border-radius: 12px;
            overflow-y: scroll;
            padding: 24px;
            box-sizing: border-box;

           // margin: 8px;
            background: white;
            box-shadow: 12px 18px 36px rgba(#030025, .2), inset -8px 8px 8px rgba(#030025, .02);
		}
	}
</style>
