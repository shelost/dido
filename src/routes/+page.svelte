<script>
	import Counter from './Counter.svelte';
	import Number from './Number.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcomeFallback from '$lib/images/svelte-welcome.png';
	import NumberFlow, { continuous } from '@number-flow/svelte'
	import {writable} from 'svelte/store'
	import {
		blur,
		crossfade,
		draw,
		fade,
		fly,
		scale,
		slide
	} from 'svelte/transition';

	import Chart from '$lib/components/Chart.svelte'
	import Table from '$lib/components/Table.svelte'
	import Phone from '$lib/components/Phone.svelte'

	let show = writable(false)
	let modal = writable(false)
	let Modal, Flow

	setTimeout(() => {
		show.set(true)
	}, 100);



	// Delays
	let d = []
	for (let i=0; i<100; i++){
		d.push(40*i)
	}

	// Numbers
	let val = 0
	let val2 = 0
	setTimeout(() => {
		val = 54697
	}, 300);
	setTimeout(() => {
		val2 = 15342
	}, 500);

	// Customers
	let Customers = [
		{
			img: '',
			name: 'John Hu',
			email: 'john@stanwith.me'
		},
		{
			img: '',
			name: 'Vitalii Dodonov',
			email: 'vitalii@stanwith.me'
		},
		{
			img: '',
			name: 'Heewon Ahn',
			email: 'shelost.off@gmail.com'
		}
	]



    function parallaxScroll(){
        let scroll = window.scrollY
    }

    window.addEventListener('scroll', parallaxScroll)


</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>


<section id = 'app'>


<section>
	<div class = 'title'>
		<h1> Dido UI </h1>
		<h2> A More Elegant Component Library </h2>
	</div>
</section>


{#if $show}
<section class = 'bento'>

	<div class = 'card a1'  in:fly={{y: 100}}>


		<Chart />
	</div>

	<div class = 'card a2'  in:fly={{y: 100, delay: d[1]}}>

		<Cashout />

	</div>

	<div class = 'card a3 phone'  in:fly={{y: 100, delay: d[2]}}>

		<Phone />

	</div>

	<div class = 'card a4'  in:fly={{y: 100, delay: d[3]}}>
		<div class = 'head'>
			<h2> February <span> 2025 </span> </h2>
		</div>
		<div class = 'calendar'>
			{#each [...Array(27).keys()] as i}
				<div class = 'day' class:active={i === 11}>
					<p> {i+1} </p>
				</div>
			{/each}
		</div>
	</div>

	<div class = 'card a5'  in:fly={{y: 100, delay: d[4]}}>

        <div class = 'head'>
            <h2> Input  </h2>
        </div>

        <div class = 'list'>
            <input type = 'text' class = 'icon-input search' placeholder = 'Search...' />
            <input type = 'text' class = 'icon-input positive' placeholder = 'Positive' value='Success!' />
            <input type = 'text' class = 'icon-input negative' placeholder = 'Negative' value='Error!' />
            <input type = 'text' class = 'icon-input disabled' placeholder = 'Disabled' disabled/>
        </div>

        <!--

		<h2> Slider</h2>
		<div class="control-row">
			<h3 class = 'label'> Advanced Settings </h3>
			<input type="range" id="rotationZ" min="-180" max="180" step="1"
			/>
			<input type="number" min="-180" max="180"
			/>
		  </div>
        -->

	</div>

	<div class = 'card a6'  in:fly={{y: 100, delay: d[5]}}>

        <div class = 'head'>
            <h2> Buttons </h2>
        </div>

        <div class = 'list'>
            <button class = 'button primary'>
                <h2> Primary Button </h2>
            </button>
            <button class = 'button secondary'>
                <h2> Secondary Button </h2>
            </button>
            <button class = 'button tertiary'>
                <h2> Tertiary Button </h2>
            </button>
            <button class = 'button mini'>
                <h2> Click Me! </h2>
            </button>
        </div>




	</div>

	<div class = 'card a7'  in:fly={{y: 100, delay: d[6]}}>

        <div class = 'head'>
            <h1> Orders </h1>
        </div>


		<Table />

	</div>


    <div class = 'card a8' in:fly={{y: 100, delay: d[7]}}>
        <div class = 'head'>
            <h2> Toggle </h2>
        </div>
        <div class = 'list'>

            <div class="toggle">
                <label class="toggle-switch">
                    <h3 class = 'label'> Advanced Settings </h3>
                    <input type="checkbox" checked>
                    <span class="toggle-slider"></span>
                </label>
            </div>

            <div class="toggle">
                <label class="toggle-switch">
                    <h3 class = 'label'> Advanced Settings </h3>
                    <input type="checkbox">
                    <span class="toggle-slider"></span>
                </label>
            </div>

        </div>
    </div>

    <div class = 'card a9' in:fly={{y: 100, delay: d[8]}}>
        <div class = 'head'>
            <h2> Customers </h2>
        </div>
        {#each Customers as c}
			<div class = 'entry'>
				<div class = 'profile'>
					<div class = 'avatar' style='background-image: url("avatar.svg")'></div>
					<div class = 'expo'>
						<h1> {c.name} </h1>
						<h2> {c.email} </h2>
					</div>
				</div>
				<button class = 'small'>
					<h3> View </h3>
				</button>
			</div>
		{/each}
    </div>


</section>
{/if}


<div id="flow-container">
    <div id = 'flow' bind:this={Flow}></div>
</div>

{#if $modal}

	<div id = 'dark' transition:fade={{duration: 200}} ></div>
	<div id = 'pop' on:click={closeModal}>
		<div id = 'bar'  in:fade={{delay: 300}}>
			<h2>
				Title
			</h2>
			<div id = 'circles'>
			</div>
		</div>
        <div id = 'modal' bind:this={Modal} in:fade={{delay: 300}}>
		</div>
	</div>

{/if}

</section>


<style lang="scss">

	@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&family=DM+Serif+Display:ital@0;1&family=EB+Garamond:ital,wght@0,400..800;1,400..800&family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&family=Lora:ital,wght@0,400..700;1,400..700&family=Newsreader:ital,opsz,wght@0,6..72,200..800;1,6..72,200..800&family=Playfair+Display:ital,wght@0,400..900;1,400..900&family=Plus+Jakarta+Sans:ital,wght@0,200..800;1,200..800&display=swap');

    $dark:  #0d1852;

	:global(number-flow-svelte) {
		--number-flow-char-height: 0.85em;
		font-size: 52px;
		letter-spacing: -2.5px;
		font-weight: 700;
		font-family: 'Inter', sans-serif;
		color: $dark;
	}

	#app{
		width: 100%;
        color: $dark;
	}

	.phone{
		padding: 0 !important;
	}


    .list{
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        margin: 6px 0;
        width: 100%;
    }


    .toggle{
        width: 100%;
    }

	.toggle-switch {
		position: relative;
		display: inline-flex;
		align-items: center;
		cursor: pointer;
        width: 100%;
        justify-content: space-between;
        margin: 6px 0;

		input {
			opacity: 0;
			width: 0;
			height: 0;
		}
	}

  	.toggle-slider {
		position: relative;
		display: inline-block;
		width: 38px;
		height: 24px;
		background-color: #ccc;
		border-radius: 24px;
		transition: 0.4s;
		box-shadow: inset -1px 2px 4px rgba(#030025, .1);

		&:before {
			position: absolute;
			content: "";
			height: 18px;
			width: 18px;
			left: 3px;
			bottom: 3px;
			background-color: white;
			border-radius: 50%;
			transition: 0.4s;
			box-shadow: 2px 4px 8px rgba(#030025, .4), inset -1px -2px 3px rgba(#030025, .25);
		}
	}

	input:checked + .toggle-slider {
		background-color: #6355FF;
	}

	input:checked + .toggle-slider:before {
		transform: translateX(14px);
		box-shadow: 2px 4px 8px rgba(#030025, .8), inset -1px -2px 3px rgba(#030025, .25);
	}

	.entry{
		display: flex;
		align-items: center;
		justify-content: space-between;
		.profile{
			display: flex;
			align-items: center;
			gap: 8px;
			padding: 8px 0;
			.avatar{
				width: 40px;
				height: 40px;
				background: rgba(black, .08);
				border-radius: 20px;
				background-size: cover;
			}
			.expo{
				h1{
					font-size: 14px;
					font-weight: 600;
					margin-bottom: 2px;
				}
				h2{
					font-size: 12px;
					font-weight: 400;
					color: rgba(black, 0.4);
				}
			}
		}
	}

	button{
		display: flex;
		align-items: center;
		border: 1px solid rgba(black, .2);
		border-radius: 6px;
		background: rgba(black, .05);
		transition: .2s ease;
		cursor: pointer;
		&.small{
			height: 32px;
			padding: 0 10px;
			h3{
				font-size: 12px;
				font-weight: 500;
				letter-spacing: -.25px;
				line-height: 100%;
			}
			&:hover{
				background: rgba(black, .09);
			}
		}
	}



	.head{
		margin-bottom: 8px;
		span{
			font-weight: 300;
            letter-spacing: -0.6px;
		}
	}

	.calendar{
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		text-align: center;
		gap: 6px;
        margin-top: 12px;

		.day{
			display: flex;
			justify-content: center;
			align-items: center;
			aspect-ratio: 1;
			border-radius: 50%;
			line-height: 100%;
			background: white;
			box-shadow: -2px 6px 15px rgba(#030025, 0.08), inset -2px -2px 4px rgba(#030025, 0.08);
			pointer-events: none;

			p{
				font-size: 13px;
				font-weight: 500;
			}

			&.active{
				background: #6355FF;
				box-shadow: -2px 6px 15px rgba(#030025, 0.36), inset -2px -4px 6px rgba(#030025, 0.1), inset 2px 4px 6px rgba(white, 0.24);
				p{
					color: white;
				}

			}
		}

	}

    input[type="text"]{
        border: 1px solid rgba($dark, .15);
        border-radius: 10px;
        background: #f8faff;
        color: $dark;

        width: 100%;
        box-sizing: border-box;
        outline: none;

        font-family: 'Plus Jakarta Sans', sans-serif;
        font-size: 14px;
        font-weight: 600;
        letter-spacing: -.1px;
        padding: 12px 14px;
        margin: 4px 0;
        transition: .2s ease;
        box-shadow: -2px 8px 8px rgba($dark, .05), inset 1px 2px 3px rgba(white, .5), inset -1px -3px 8px rgba($dark, .03);
		box-shadow: -2px 8px 8px rgba($dark, .0), inset 2px 4px 8px rgba($dark, .1), inset -1px -3px 8px rgba(white, .1);

        &.icon-input{
            background-image: url('/icon-search.svg');
            background-size: 18px;
            background-position: 10px 50%;
            background-repeat: no-repeat;
            padding-left: 32px;
        }

        &.positive{
            //background: rgba(#0fba59, .2);
            border: 1px solid rgba(#0fba59, 1);
            background-image: url('/icon-check.svg');
            background-size: 18px;
            background-position: 10px 50%;
            background-repeat: no-repeat;
        }

        &.negative{
            //background: rgba(#ff0000, .12);
            border: 1px solid rgba(#ff0000, 1);
            background-image: url('/icon-x.svg');
            background-size: 18px;
            background-position: 10px 50%;
            background-repeat: no-repeat;
        }



        &:focus{
            box-shadow: -2px 8px 8px rgba(black, .0), inset 1px 4px 8px rgba($dark, .1), inset -1px -3px 8px rgba(white, .03);

            border: 1px solid rgba(#6355FF, .5);
        }

        &::placeholder{
            color: rgba($dark, .4);
        }

        &:disabled{
            background: rgb(229, 229, 248);
        }
    }

	input[type="range"] {
		-webkit-appearance: none;
		width: 100%;
		height: 32px;
		padding: 0 2px;
		background: rgba(#030025, .08);
		background: rgba(#6355FF, .2);
		border-radius: 10px;
		outline: none;
		//box-shadow: 4px 8px 12px rgba(black, .15);

		&::-webkit-slider-thumb {
			-webkit-appearance: none;
			width: 14px;
			height: 26px;
			border-radius: 10px;
			background: rgba(white, .9);
			border: 2px solid white;
			cursor: pointer;
			// border: 1.5px solid rgba(white, .9);
			box-shadow: -2px 4px 12px rgba(#030025, .3), inset -2px -2px 3px rgba(#030025, .08);
			backdrop-filter: blur(10px);
			transition: .2s ease;

			&:hover{
				transform: scale(1.08);
			}
		}
	}

	.number{
		color: black;
		font-size: 100px;
	}

	.button{
		background: #6355FF;
		width: fit-content;
		color: white;
		text-align: center;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10px;
		padding: 10px 18px 11px 18px;
		box-shadow: -2px 8px 8px rgba($dark, .3), inset 1px 2px 3px rgba(white, .15), inset -1px -3px 6px 2px rgba($dark, .2);
        margin: 4px 0;
		transition: .2s ease;
		cursor: pointer;

		h2{
			font-size: 14px;
			font-weight: 600;
			color: white;
			font-family: 'Plus Jakarta Sans', sans-serif;
            text-shadow: -2px 4px 8px rgba(black, .1);
			letter-spacing: -.1px;
			transition: .2s ease;
		}

		&:hover{
			box-shadow: -2px 8px 12px rgba(black, .08), inset 0px 4px 8px 2px rgba(black, .3), inset -2px -3px 6px rgba(white, .1);
			h2{
				transform: translateY(.3px);

			}
		}

        &.primary{
            h2{
                text-shadow: -2px 4px 8px rgba(black, .3);
            }
            &:hover{
                h2{
                    text-shadow: -2px 4px 8px rgba(black, .2);
                }
            }
        }

		&.secondary{
			border: 1px solid rgba(#6355FF, 1);
			background: rgba(white, 0);
			color: #6355FF;
			box-shadow: -2px 8px 8px rgba(black, .1), inset 1px 2px 3px rgba(white, .15), inset -1px -3px 8px rgba(#030025, .1);

			h2{
				color: #6355ff;
			}

			&:hover{
				box-shadow: -2px 8px 8px rgba(black, .0), inset 0px 6px 8px rgba(#030025, .15), inset -2px -3px 6px rgba(white, .1);
			}
		}

        &.tertiary{
            background: #d6e0ff;
			border: 1px solid #d6e0ff;
            color: #6355FF;
            box-shadow: -2px 8px 8px rgba(black, .08), inset 1px 2px 3px rgba(white, .15), inset -1px -3px 6px rgba(#030025, .05);

            h2{
                color: $dark;
            }

            &:hover{
                box-shadow: -2px 8px 8px rgba(black, .0), inset 1px 4px 6px 2px rgba($dark, .1), inset -1px -3px 8px rgba(white, .08);
            }
        }

        &.mini{
            background: $dark;
            padding: 7px 12px 8px 12px;
            border: 1px solid rgba(black, .1);
            box-shadow: -2px 8px 8px rgba(black, .08), inset 1px 2px 3px rgba(white, .25), inset -1px -3px 8px rgba(#030025, .9);

            margin: 8px 0;

            h2{
                font-size: 13px;
            }
        }
	}


	.card{
		width: 100%;
		background: white;
		//border: 2px solid white;
		border-radius: 16px;
		box-shadow: -10px 30px 40px rgba($dark, 0.25), inset -1px -2px 2px rgba($dark, 0.04);
		box-sizing: border-box;
		padding: 20px;
		margin: 0;
		position: relative;
		overflow: hidden;
        transition: .2s ease;

		display: flex;
		flex-direction: column;


		&.a1{
			grid-column: 1 / 3;
		}
        &.a2{
            .button{
                width: 100%;
            }
        }
		&.a3{
			grid-column: 4;
			grid-row: 1/3;
		}
		&.a7{
			grid-column: 1 / 4;
			grid-row: 3 / 5;
		}

        &:hover{
            transform: translateY(-0px) scale(1.005);
            box-shadow: -20px 30px 40px rgba(#030025, 0.15), inset -2px -4px 4px rgba(#030025, 0.03);
        }
	}



	section{
		width: 95vw;
		max-width: 1300px;
		margin: auto;
	}

	.title{
		padding: 64px 0 32px 0;
		h1{
			font-family: 'Plus Jakarta Sans', sans-serif;
			font-size: 44px;
			font-weight: 900;
			letter-spacing: -1.4px;
			color: #171255;
			margin-bottom: 2px;
		}
		h2{
			font-size: 20px;
			font-weight: 500;
			letter-spacing: -.6px;
			color: rgba(#171255, .5);
		}
	}

    #app{
        width: clamp(300px, 100%, 1200px);
    }

	.bento{
        width: 100%;
		gap: 28px;
		//border: 1px solid red;
		display: grid;
		padding: 0;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: repeat(4, 280px);
		margin-bottom: 100px;
	}

	h1 {
		font-family: 'Inter', sans-serif;
		font-weight: 750;
		font-size: 28px;
		letter-spacing: -0.4px;
        color: $dark;
	}

	h2{
		font-size: 18px;
		font-weight: 700;
		letter-spacing: -0.3px;
        color: $dark;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}



	@media screen and (max-width: 1024px){

		.card{
			border: 1px solid blue;
		}
	}

	@media screen and (max-width: 768px){

		.card{
			border: 1px solid red;
		}
	}

</style>
