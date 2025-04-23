<script>
	import Chart from '$lib/components/Chart.svelte'
	import Table from '$lib/components/Table.svelte'
    import Cashout from '$lib/components/Cashout.svelte'

    import { fly } from 'svelte/transition';

</script>

<div class = 'page'>

    <div class = 'top'>
        <div class = 'chart' in:fly={{y: 50, delay: 100}}>
            <Chart />
        </div>

        <div class = 'cashout card'>
            <Cashout />
        </div>
    </div>

    <div class = 'table card' in:fly={{ y: 25, duration: 400 }}>
        <Table title='Orders'/>
    </div>
</div>

<style lang="scss">

    .top{
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: flex-start;
        gap: 24px;
        margin-top: 24px;

        .chart{
            flex: 1;
            height: 250px;
            padding: 24px;
        }

        .cashout{
            width: 300px;
        }
    }

</style>