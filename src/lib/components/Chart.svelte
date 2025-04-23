<script>
    import { onMount } from 'svelte';
    import NumberFlow, { continuous } from '@number-flow/svelte';

    export let value = 54697;
    export let title = "Total Revenue";
    export let gradientColors = ['#6355FF', 'rgba(100,85,225,0.5)', 'rgba(100,85,225,0)'];

    let chartElement;
    let chart = null; // Initialize as null to check existence
    let val = 0;
    let ApexCharts;
    let containerHeight;
    let chartContainer;
    let headerElement;
    let isChartInitialized = false; // Flag to track initialization status

    // Generate realistic-looking data where the trend is always up or flat
    function generateUpwardData(finalValue, pointCount = 20) {
        const data = [];
        let currentValue = 0;
        const minStep = 0; // Minimum step (flat)
        const maxStep = finalValue / (pointCount * 0.7); // Maximum step size

        for (let i = 0; i < pointCount; i++) {
            // Generate random step that's always positive or zero
            const step = Math.random() * maxStep + minStep;

            // Make sure we don't exceed the final value
            if (currentValue + step > finalValue && i < pointCount - 1) {
                // If we're about to exceed the final value, generate a smaller step
                currentValue += (finalValue - currentValue) * (Math.random() * 0.3);
            } else if (i === pointCount - 1) {
                // Make sure the last point exactly matches the final value
                currentValue = finalValue;
            } else {
                currentValue += step;
            }

            data.push({
                x: new Date().setDate(new Date().getDate() - (pointCount - i)),
                y: Math.round(currentValue)
            });
        }

        return data;
    }

    function getHeaderFullHeight() {
        if (!headerElement) return 0;

        // Get the computed style of the header to properly account for margins
        const headerStyle = window.getComputedStyle(headerElement);
        const headerRect = headerElement.getBoundingClientRect();

        // Include margins in the total height calculation
        const marginBottom = parseInt(headerStyle.marginBottom, 10) || 0;

        // Return the total header height including its margin
        return headerRect.height + marginBottom;
    }

    // Clean up any existing chart
    function cleanupChart() {
        if (chart) {
            try {
                chart.destroy();
                chart = null;

                // Also clear the chart element's contents
                if (chartElement) {
                    chartElement.innerHTML = '';
                }

                isChartInitialized = false;
            } catch (error) {
                console.error('Error destroying chart:', error);
            }
        }
    }

    function updateChartSize() {
        if (!chart || !chartElement || !chartContainer || !headerElement || !isChartInitialized) return;

        try {
            // Get the total container dimensions
            const containerRect = chartContainer.getBoundingClientRect();

            // Get header's full height including margin
            const headerFullHeight = getHeaderFullHeight();

            // Calculate available height (total height minus header full height)
            const availableHeight = containerRect.height - headerFullHeight;

            console.log('Container height:', containerRect.height);
            console.log('Header height:', headerFullHeight);
            console.log('Available height:', availableHeight);

            // Apply the corrected dimensions to the chart
            chart.updateOptions({
                chart: {
                    height: Math.max(availableHeight, 50), // Ensure minimum height
                    width: containerRect.width
                }
            }, false, false); // Don't animate or redraw immediately

            // Set explicit dimensions directly on the DOM element
            if (chartElement.querySelector('.apexcharts-canvas')) {
                const canvasEl = chartElement.querySelector('.apexcharts-canvas');
                canvasEl.style.height = `${availableHeight}px`;
                canvasEl.style.width = `${containerRect.width}px`;
            }
        } catch (error) {
            console.error('Error updating chart size:', error);
        }
    }

    async function initializeChart() {
        // Don't initialize if already done or if required elements are missing
        if (isChartInitialized || !chartElement || !headerElement || !chartContainer) return;

        try {
            // Clean up any existing chart first
            cleanupChart();

            const seriesData = generateUpwardData(value);

            // Get header's full height including margin
            const headerFullHeight = getHeaderFullHeight();

            // Get container dimensions
            const containerRect = chartContainer.getBoundingClientRect();

            // Calculate available height
            const availableHeight = containerRect.height - headerFullHeight;

            console.log('Initial container height:', containerRect.height);
            console.log('Initial header height:', headerFullHeight);
            console.log('Initial available height:', availableHeight);

            const options = {
                chart: {
                    type: 'area',
                    height: Math.max(availableHeight, 50),
                    width: containerRect.width,
                    fontFamily: 'inherit',
                    toolbar: {
                        show: false
                    },
                    animations: {
                        enabled: true,
                        easing: 'easeinout',
                        speed: 800,
                        animateGradually: {
                            enabled: true,
                            delay: 150
                        },
                        dynamicAnimation: {
                            enabled: true,
                            speed: 350
                        }
                    },
                    parentHeightOffset: 0
                },
                colors: ['#6355FF'], // Set the primary line color
                dataLabels: {
                    enabled: false
                },
                stroke: {
                    curve: 'smooth',
                    width: 3,
                    colors: ['#6355FF'] // Explicitly set the stroke color
                },
                series: [{
                    name: title,
                    data: seriesData
                }],
                fill: {
                    type: 'gradient',
                    gradient: {
                        shadeIntensity: 1,
                        opacityFrom: 0.7,
                        opacityTo: 0.2,
                        stops: [0, 90, 100],
                        colorStops: [
                            {
                                offset: 0,
                                color: gradientColors[0],
                                opacity: 0.8
                            },
                            {
                                offset: 50,
                                color: gradientColors[1] || gradientColors[0],
                                opacity: 0.6
                            },
                            {
                                offset: 100,
                                color: gradientColors[2] || gradientColors[0],
                                opacity: 0.2
                            }
                        ]
                    }
                },
                grid: {
                    borderColor: 'rgba(0,0,0,0.05)',
                    strokeDashArray: 5,
                    padding: {
                        top: 5,
                        right: 0,
                        bottom: 5,
                        left: 0
                    },
                    xaxis: {
                        lines: {
                            show: false
                        }
                    },
                    yaxis: {
                        lines: {
                            show: false
                        }
                    }
                },
                xaxis: {
                    type: 'datetime',
                    labels: {
                        format: 'dd MMM',
                        style: {
                            colors: 'rgba(0,0,0,0.6)'
                        }
                    },
                    axisBorder: {
                        show: false
                    },
                    axisTicks: {
                        show: false
                    },
                    tooltip: {
                        enabled: false
                    }
                },
                yaxis: {
                    floating: true,
                    show: false,
                    axisTicks: {
                        show: false
                    },
                    axisBorder: {
                        show: false
                    },
                    labels: {
                        show: false
                    },
                    min: 0,
                    max: value * 1.1, // Still keep the max value for proper scaling
                },
                tooltip: {
                    x: {
                        format: 'dd MMM yyyy'
                    },
                    y: {
                        formatter: function(val) {
                            return '$' + val.toLocaleString();
                        }
                    },
                    theme: 'light'
                },
                legend: {
                    show: false
                },
                responsive: [{
                    breakpoint: 3000,
                    options: {
                        chart: {
                            height: '100%'
                        }
                    }
                }]
            };

            // Create chart with precise dimensions
            chart = new ApexCharts(chartElement, options);
            await chart.render();
            isChartInitialized = true;

            // Directly set explicit dimensions on the chart element for reinforcement
            if (chartElement.querySelector('.apexcharts-canvas')) {
                const canvasEl = chartElement.querySelector('.apexcharts-canvas');
                canvasEl.style.height = `${availableHeight}px`;
                canvasEl.style.width = `${containerRect.width}px`;
            }
        } catch (error) {
            console.error('Error initializing chart:', error);
            cleanupChart(); // Cleanup on error
        }
    }

    onMount(async () => {
        // Import ApexCharts dynamically for SSR compatibility
        ApexCharts = (await import('apexcharts')).default;

        // Wait for the DOM to be fully updated
        setTimeout(async () => {
            try {
                await initializeChart();

                // Animate the value with NumberFlow
                val = value;
            } catch (error) {
                console.error('Error in onMount initialization:', error);
            }
        }, 50); // Increased timeout to ensure DOM is fully rendered

        // Update chart when container resizes
        const resizeObserver = new ResizeObserver(() => {
            if (chart && isChartInitialized) {
                // Debounce the resize handling
                clearTimeout(window.resizeTimer);
                window.resizeTimer = setTimeout(() => {
                    updateChartSize();
                }, 100);
            }
        });

        if (chartContainer) {
            resizeObserver.observe(chartContainer);
        }

        return () => {
            if (window.resizeTimer) {
                clearTimeout(window.resizeTimer);
            }
            resizeObserver.disconnect();
            cleanupChart();
        };
    });
</script>

<div class="chart" bind:this={chartContainer}>
    <div class="header" bind:this={headerElement}>
        <h3 class="label">{title}</h3>
        <NumberFlow
            value={val}
            format={{ style: 'currency', currency: 'USD', trailingZeroDisplay: 'stripIfInteger' }}
            plugins={[continuous]}
            class='number'
            transformTiming={{
                delay: 100,
                duration: 1000,
                easing: 'linear(0, 0.0012, 0.0048 0.97%, 0.0195 2.03%, 0.0446 3.19%, 0.0806 4.48%, 0.1581 6.77%, 0.3679 12.32%, 0.469 15.16%, 0.5199 16.71%, 0.5665, 0.6097, 0.6496 21.26%, 0.6876, 0.7222 24.42%, 0.7541 26.03%, 0.7833 27.68%, 0.8104 29.39%, 0.8352 31.16%, 0.8575 32.97%, 0.8779 34.87%, 0.897 36.93%, 0.9142 39.13%, 0.9292 41.42%, 0.9424 43.84%, 0.9539 46.42%, 0.9637 49.16%, 0.972 52.13%, 0.979 55.39%, 0.9888 62.39%, 0.995 71.16%, 0.9983 82.61%, 0.9997 100%)'
            }}
        />
    </div>
    <div class="chart-container" bind:this={chartElement}></div>
</div>

<style lang="scss">
    .chart {
        font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        width: 100%;
        height: 100%;
        background-color: white;
        border-radius: 8px;
        overflow: hidden;
        display: flex;
        flex-direction: column;
        box-sizing: border-box;
    }



    .number {
        font-size: 24px;
        font-weight: 600;
        color: #333;
    }

    .chart-container {
        flex: 1;
        width: 100%;
        min-height: 0; /* Important for flex children to prevent overflow */
        position: relative;
        overflow: hidden;
        box-sizing: border-box;
        padding: 0; /* Ensure no padding is affecting chart size */
    }

    /* Target ApexCharts DOM elements to ensure they stay contained */
    :global(.apexcharts-canvas) {
        width: 100% !important;
        height: 100% !important;
        position: absolute !important;
        top: 0 !important;
        left: 0 !important;
    }

    :global(.apexcharts-inner) {
        transform: translate(0, 0) !important;
    }

    /* Ensure chart has proper spacing at the bottom */
    :global(.apexcharts-graphical) {
        padding-bottom: 5px;
    }
</style>