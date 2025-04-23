<script>
    import { fly } from 'svelte/transition';
	import Chart from '$lib/components/Chart.svelte'
	import Table from '$lib/components/Table.svelte'


</script>

<div class = 'page'>
	<Chart />

    <div class = 'cards'>
        <div class = 'table card' in:fly={{y:50, delay: 100}}>
            <Chart value = {100} />
        </div>
        <div class = 'table card' in:fly={{y:50, delay: 200}}>
            <Chart value = {57.9} />
        </div>
        <div class = 'table card' in:fly={{y:50, delay: 300}}>
            <Chart value = {499.99} />
        </div>
        <div class = 'table card' in:fly={{y:50, delay: 400}}>
            <Chart value = {2000} s/>
        </div>
    </div>

</div>

<style lang="scss">
    .cards{
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 0px;
    }

    .card{
        height: 280px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 20px;
    }
</style>