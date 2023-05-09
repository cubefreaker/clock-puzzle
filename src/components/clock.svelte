<script>
    export let deg;
    export let index;
</script>

<div id="clock-{index}" class="relative bg-blue-500 w-96 h-96 rounded-full">
    {#each [...Array(10).keys()] as i}
        <div class="absolute w-[20px] h-[10%] top-[40%] left-[49%]" style="transform: rotate({i*30}deg)">TES</div>
    {/each}
    <div id="needle-{index}" class="w-[10px] h-[40%] bg-black absolute top-[10%] left-[49%] origin-bottom transition-all" style="transform: rotate({deg}deg)"></div>
</div>