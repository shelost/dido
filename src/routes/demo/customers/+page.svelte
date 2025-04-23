<script>
	import Chart from '$lib/components/Chart.svelte'
	import Table from '$lib/components/Table.svelte'

    import { fly } from 'svelte/transition'

</script>

<div class = 'page'>
    <div class = 'table card' in:fly={{ y: 25, duration: 400 }}>
        <Table title = 'Customers' />
    </div>
</div>

<style lang="scss">
    .page{

    }
</style>