<script>
    import Clock from '../components/clock.svelte';
    let deg = 0;
    let intervalPlus;
    let intervalMinus;

    function degPlus() {
        deg += 30;
        intervalPlus = setInterval(() => {
            deg += 30;
        }, 150);
    }

    function degMinus() {
        deg -= 30;
        intervalMinus = setInterval(() => {
            deg -= 30;
        }, 150);
    }
</script>

<section class="w-screen h-screen bg-teal-200 flex place-items-center justify-center">
    <div class="top-0 w-screen fixed flex justify-between">
        <button class="m-4 px-4 py-1 bg-green-500 rounded-lg" on:mousedown={degMinus} on:mouseup={clearInterval(intervalMinus)}>Rotate Left</button>
        <button class="m-4 px-4 py-1 bg-green-500 rounded-lg" on:mousedown={degPlus} on:mouseup={clearInterval(intervalPlus)}>Rotate Right</button>
    </div>
    <Clock index={1} deg={deg}/>
</section>