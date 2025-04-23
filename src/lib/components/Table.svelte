<script>
    import { fly } from 'svelte/transition';
    import { onMount } from 'svelte';

    export let title = 'Table';

    export let Rows = [
		{
			date: 'Date',
			time: '',
			email: 'Email',
			product: 'Product',
			amount: 'Amount'
		},
		{
			date: 'Apr 7',
			time: '9:31 AM',
			email: 'john@stanwith.me',
			product: '1:1 Coaching Session',
			amount: '40.00'
		},
		{
			date: 'Apr 7',
			time: '9:31 AM',
			email: 'vitalii@stanwith.me',
			product: 'My Creator Course',
			amount: '40.00'
		},
		{
			date: 'Apr 5',
			time: '9:31 AM',
			email: 'heewon@stanwith.me',
			product: '1:1 Coaching Session',
			amount: '40.00'
		},
		{
			date: 'Apr 3',
			time: '9:31 AM',
			email: 'shiva@stanwith.me',
			product: '1:1 Coaching Session',
			amount: '40.00'
		},
		{
			date: 'Mar 29',
			time: '9:31 AM',
			email: 'brydon@stanwith.me',
			product: 'My Creator Course',
			amount: '40.00'
		},
		{
			date: 'Mar 29',
			time: '9:31 AM',
			email: 'karin@stanwith.me',
			product: 'Digital Product Kit',
			amount: '40.00'
		},
        {
			date: 'Apr 3',
			time: '9:31 AM',
			email: 'shiva@stanwith.me',
			product: '1:1 Coaching Session',
			amount: '40.00'
		},
		{
			date: 'Mar 29',
			time: '9:31 AM',
			email: 'brydon@stanwith.me',
			product: 'My Creator Course',
			amount: '40.00'
		},
		{
			date: 'Mar 29',
			time: '9:31 AM',
			email: 'karin@stanwith.me',
			product: 'Digital Product Kit',
			amount: '40.00'
		}
	]

    // Animation control
    let visible = false;

    onMount(() => {
        // Trigger animations after component is mounted
        visible = true;
    });
</script>

<div class = 'table'>
    <div class = 'title'>
        <h2> {title} </h2>
    </div>
    {#each Rows as r, i (i)}
        {#if visible || i === 0}
            <div class = 'row' class:first={i === 0} in:fly={{y: 20, duration: 400, delay: 50+i * 30}}>
                <div class = 'date flex'>
                    <h2> {r.date} </h2>
                    <h3> {r.time} </h3>
                </div>
                <div class = 'email flex'>
                    <h2> {r.email} </h2>
                </div>
                <div class = 'product flex'>
                    <h2> {r.product} </h2>
                </div>
                <div class = 'amount flex'>
                    {#if i === 0}
                        <h2> {r.amount} </h2>
                    {:else}
                        <h2> ${r.amount} </h2>
                    {/if}
                </div>
            </div>
        {/if}
    {/each}
</div>

<style lang="scss">

    $dark: #08124b;

    .title{
        margin-bottom: 24px;
        h2{
            font-size: 24px;
            font-weight: 700;
            letter-spacing: -.4px;
            margin: 0;
            color: $dark;
        }
    }

    .table{


		.row{
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 12px 6px;
			//border-bottom: 1px solid rgba(black, .1);
			transition: .2s ease;


			//box-shadow: -4px 8px 12px rgba($dark, .08), inset 1px 2px 3px rgba(white, .15), inset -1px -3px 8px rgba($dark, .03);
			margin: 4px 0;
			border-radius: 8px;

			cursor: pointer;

			h2{
				font-size: 14px;
				font-weight: 500;
                letter-spacing: -.25px;
			}
			h3{
				font-size: 13px;
				font-weight: 500;
				letter-spacing: -.5px;
				color: rgba(#08124b, .4);
			}

			.date{
				flex: 2;
			}
			.email{
				flex: 3;
			}
			.product{
				flex: 4;
			}
			.amount{
				flex: 1;
				justify-content: flex-end;
				h2{
					font-weight: 600;
					color: #0fba59;
				}
			}

			.flex{
				display: flex;
				align-items: center;
				gap: 6px;
			}

			&:hover{
				//transform: scale(1.008);
                background: white;
                transform: translateY(-.5px);
				border-radius: 8px;
				//background: #f0f0f4;
				box-shadow: -2px 8px 16px rgba($dark, .08), inset 1px 2px 3px rgba(white, .15), inset -1px -3px 8px rgba($dark, .03);
			}

			&.first{
				background: none;
				h2{
					color: #8e8dab;
				}
			}
		}
	}
</style>