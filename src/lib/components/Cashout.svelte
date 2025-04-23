<script>
   import NumberFlow, { continuous } from '@number-flow/svelte'
   import { fly } from 'svelte/transition';
   import { onMount } from 'svelte';

   let val = 0

   let val2 = 1974.02

   onMount(() => {
    setTimeout(() => {
        val = val2
    }, 100)
   })
</script>

<div class = 'cashout'>
    <div class = 'cash'>
        <h3 class = 'label'> Available Funds </h3>
        <NumberFlow
            value={val}
            format={{ style: 'currency', currency: 'USD', trailingZeroDisplay: 'stripIfInteger' }}
            trend={1}
            class='number'
            transformTiming={{
                // Used for layout-related transforms:
                delay: 100,
                duration: 1600,
                easing: 'linear(0, 0.0012, 0.0048 0.97%, 0.0195 2.03%, 0.0446 3.19%, 0.0806 4.48%, 0.1581 6.77%, 0.3679 12.32%, 0.469 15.16%, 0.5199 16.71%, 0.5665, 0.6097, 0.6496 21.26%, 0.6876, 0.7222 24.42%, 0.7541 26.03%, 0.7833 27.68%, 0.8104 29.39%, 0.8352 31.16%, 0.8575 32.97%, 0.8779 34.87%, 0.897 36.93%, 0.9142 39.13%, 0.9292 41.42%, 0.9424 43.84%, 0.9539 46.42%, 0.9637 49.16%, 0.972 52.13%, 0.979 55.39%, 0.9888 62.39%, 0.995 71.16%, 0.9983 82.61%, 0.9997 100%)'
            }}
        />
    </div>
    <div class = 'buttons'>
        <button class = 'button primary'  in:fly={{y: 50, delay: 100}}>
            <h2> Cash Out </h2>
        </button>
        <button class = 'button secondary'  in:fly={{y: 50, delay: 200}}>
            <h2> Settings </h2>
        </button>
    </div>
</div>

<style lang="scss">

    $dark:  #0d1852;

    :global(.cashout number-flow-svelte) {
		--number-flow-char-height: 0.85em;
		font-size: 44px;
		letter-spacing: -1px;
		font-weight: 650;
		font-family: 'Inter', sans-serif;
		color: $dark;
	}

    .cashout{
        display: flex;
        flex-direction: column;
        gap: 24px;
    }

    .buttons{
        display: flex;
        flex-direction: column;
        gap: 2px;
    }

    .cash{
		flex: 1;

		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

    button{
        width: 100%;
    }

</style>