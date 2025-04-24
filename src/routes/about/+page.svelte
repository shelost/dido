<script>
    import { fly } from 'svelte/transition';
</script>

<div class = 'main'>


    <div class = 'content card' in:fly={{y: 50, duration: 400, delay: 100}}>
        <h2> About </h2>
        <p>
            Dido is a simple UI component library, built in <a href = 'https://svelte.dev'>Svelte</a> but easily adaptable to other frameworks.
        </p>
        <p>
            The main aesthetic inspiration is a pseudo-3D skeuomorphic design, making the UI cards feel like real, tangible objects.
        </p>
        <p>
            This project is still in early development, and more components will be added in the future!
        </p>

        <a href = 'https://www.ahnheewon.com'>
            <img id = 'ahw' src = '/ahnheewon3.png' alt = 'Dido' />
        </a>
    </div>


</div>



<style lang='scss'>

    #ahw{
        width: fit-content;
        height: 24px;
        margin: auto;
        margin-top: 40px;
    }

.main{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;

    p{
        font-size: 15px;
        font-weight: 450;
        letter-spacing: -0.32px;
    }
}

.card{
    width: 320px;
    padding: 24px 28px;
    display: flex;
    flex-direction: column;
    align-items: center;
    h2{
        font-size: 28px;
        font-weight: 600;
        letter-spacing: -0.5px;
        margin-bottom: 8px;
    }
    p{
        font-size: 14px;
        line-height: 140%;
        margin-top: 20px;
    }
}



</style>