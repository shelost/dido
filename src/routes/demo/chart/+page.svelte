<script>
    import Chart from '$lib/components/Chart.svelte';
</script>

<div class="container">
    <h1>Chart Demo</h1>

    <div class="charts-wrapper">
        <div class="chart-box">
            <Chart
                value={54697}
                title="Total Revenue"
                gradientColors={['#4158D0', '#C850C0', '#FFCC70']}
            />
        </div>

        <div class="chart-box">
            <Chart
                value={125000}
                title="Monthly Sales"
                gradientColors={['#00b09b', '#96c93d', '#dbe6c4']}
            />
        </div>

        <div class="chart-box">
            <Chart
                value={25890}
                title="New Customers"
                gradientColors={['#fc5c7d', '#6a82fb', '#b8e1fc']}
            />
        </div>

        <div class="chart-box">
            <Chart
                value={342550}
                title="Annual Growth"
                gradientColors={['#FF416C', '#FF4B2B', '#FFB75E']}
            />
        </div>

        <div class="chart-box">
            <Chart
                value={87250}
                title="Profit Margin"
                gradientColors={['#aa4b6b', '#6b6b83', '#3b8d99']}
            />
        </div>

        <div class="chart-box">
            <Chart
                value={156789}
                title="Website Traffic"
                gradientColors={['#005C97', '#1CB5E0', '#7DE2FC']}
            />
        </div>
    </div>
</div>

<style>
    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 2rem;
    }

    h1 {
        font-size: 2rem;
        margin-bottom: 2rem;
        color: #333;
    }

    .charts-wrapper {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
        gap: 2rem;
    }

    .chart-box {
        background-color: #f5f5f5;
        border-radius: 8px;
        overflow: hidden;
    }

    @media (max-width: 768px) {
        .charts-wrapper {
            grid-template-columns: 1fr;
        }
    }
</style>