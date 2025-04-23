<script>
    import { onMount } from 'svelte';
    import { fly } from 'svelte/transition';
    import rafaella from '$lib/images/rafaella.png';

    let d = [0, 100, 200, 300, 400, 500, 600, 700, 800, 900, 1000];

    export let Products = [
        {
            name: 'Product 1',
            price: 100,
            image: 'product1.png'
        },
        {
            name: 'Product 2',
            price: 200,
            image: 'product2.png'
        },
        {
            name: 'Product 3',
            price: 300,
            image: 'product3.png'
        }
    ]
</script>

<div class = 'phone'>

    <div class = 'mast' in:fly={{y: 50, delay: d[1]}}>
        <h2> Rafaella </h2>
    </div>

    <img class = 'rafaella' src = {rafaella} alt = 'Image'  in:fly={{y: 100, delay: d[2]+20}}>


    <div class = 'products'>
        {#each Products as p, i}
            <div class = 'product' in:fly={{y: 50, delay: i*100}}>
                <div class = 'thumbnail'></div>
                <div class = 'expo'>
                    <h2> {p.name} </h2>
                    <h3> ${p.price} </h3>
                </div>
            </div>
        {/each}
    </div>

</div>

<style lang="scss">

    .phone{
		background: #17043c;
        width: 100%;
        height: 100%;
        //border-radius: 36px;
        //border: 4px solid rgba(white, .25);
        //box-shadow: -10px 20px 50px rgba(#030025, 0.7), inset -2px -4px 8px rgba(#030025, 0.08);
		.rafaella{
			height: 105%;
			position: absolute;
			bottom: 0;
			left: -15%;
            filter: drop-shadow(-6px 0px 6px rgba(#030025, 0.9));
		}

        .mast{
            padding-top: 36px;
            h2{
                font-family: 'Newsreader', serif;
                font-size: 64px;
                font-weight: 600;
                letter-spacing: -2px;
                color: #ffe5a9;
                text-align: center;
            }
        }

        .products{
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            box-sizing: border-box;
            padding: 10px 20px;
            z-index: 3;

            .product{
                padding: 12px 14px;
                background: #ffebbd;
                border-radius: 18px;
                margin: 12px 0;

                display: flex;
                align-items: center;
                transition: .2s ease;
                box-shadow: inset -2px -4px 4px rgba(#030025, 0.1);
                cursor: pointer;

                filter: drop-shadow(-6px 24px 36px rgba(#030025, 0.9));

                .thumbnail{
                    width: 36px;
                    height: 36px;
                    border-radius: 10px;
                    background: white;
                    box-shadow: -6px 12px 24px rgba(#030025, 0.2), inset 2px 2px 4px rgba(#030025, 0.1);
                    border: 1px solid white;
                    margin-right: 12px;
                }

                .expo{
                    h2{
                        font-size: 16px;
                        font-weight: 600;
                        letter-spacing: -.2px;
                    }
                    h3{
                        font-size: 14px;
                        font-weight: 450;
                        margin-top: 2px;
                        letter-spacing: -.25px;
                    }
                }

                &:hover{
                    transform: translateY(-1px) scale(1.02);
                }
            }
        }
	}
</style>