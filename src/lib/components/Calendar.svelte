<script>

</script>

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

<style lang="scss">


	.head{
		margin-bottom: 8px;

        h2{
            font-size: 20px;
            font-weight: 700;
            letter-spacing: -0.4px;
            span{
                font-size: 20px;
                font-weight: 300;
                letter-spacing: -0.6px;
            }
        }
	}

    .calendar{
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		text-align: center;
		gap: 4px;
        margin-top: 12px;

		.day{
			display: flex;
			justify-content: center;
			align-items: center;
			aspect-ratio: 1;
			border-radius: 50%;
			line-height: 100%;
			background: white;
            padding: 2px;
            cursor: pointer;
            transition: .2s ease;

			p{
				font-size: 14px;
				font-weight: 500;
			}

            &:hover{
                background: rgba(#6355FF, .1);
            }

			&.active{
				background: #6355FF;
				//box-shadow: -2px 6px 15px rgba(#030025, 0.36), inset -2px -4px 6px rgba(#030025, 0.1), inset 2px 4px 6px rgba(white, 0.24);
				p{
					color: white;
				}

			}
		}

	}

</style>