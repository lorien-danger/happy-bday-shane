<script>
    import { onMount } from 'svelte';
    import JSConfetti from 'js-confetti'


    const colors = ['text-primary', 'text-secondary', 'text-accent'];
    const size = ['text-2xl', 'text-3xl'];

    let showCard = false;
    let audio;
    let selectedColor = colors[0];
    let selectedSize = size[1];
    let scrollIndicatorPos = "bottom-10";


    function partyTime() {
        selectedColor = colors[Math.floor(Math.random() * colors.length)];
        selectedSize = selectedSize === size[0] ? size[1] : size[0];
        scrollIndicatorPos = scrollIndicatorPos === "bottom-10" ? "bottom-9" : "bottom-10";

        audio.play();
    }

    function confettiTime() {
        const jsConfetti = new JSConfetti()

        jsConfetti.addConfetti({
            confettiRadius: 5,
            confettiNumber: 300,
        })
    }

    setInterval(() => {
        if (showCard) {
            confettiTime();
        }
    }, 2000);

    setInterval(() => {
        if (showCard) {
            partyTime();
        }
    }, 250);
</script>

<div class="container mx-auto font-sans text-center flex flex-col items-center">
    <div class="h-screen flex flex-col justify-center items-center ">
        {#if !showCard}
            <h1 class="text-5xl font-bold leading-normal">Happy birthday<br>shane!</h1>
            <button on:click={() => {
                showCard = true;
                confettiTime();
            }} class="mt-10 btn btn-secondary text-xl">Click me 😉</button>
        {:else}
            <div class="card">
                <h1 class={`transition-all card-title ${selectedSize} ${selectedColor}`}>You soft cock.</h1>
            </div>
            <p class={`transition-all absolute italic ${scrollIndicatorPos}`}>[ scroll down... ]</p>
        {/if}
    </div>
    {#if showCard}
        <div class="mt-48 card md:w-1/2 pb-24">
            <div class="card-body text-left">
                <h2 class={`transition-all card-title text-2xl ${selectedColor}`}>Happy Birthday Dad/Shane</h2>
                <p class="mt-8 text-xl">
                We want you to know how proud we are of how far you’ve come in the past year.
                You’ve finally started to put yourself first and we can all see you becoming your best you again.<br><br>
                We are both so thankful that you and Mum/Amy gave us the opportunity to build our first home together. You dedicated your weekends for months to build it and we are forever grateful for that.<br><br>
                Have the bestest birthday ever, you deserve it<br><br>
                <span class="font-medium">We love you Dad/Shane ❤️</span>
                </p>
            </div>
        </div>
    {/if}
    <audio bind:this={audio} src="/party-music.mp3"></audio>
</div>