<script>
    export let deg;
    export let index;
    export let active;
    $: transform = active ? `transform: rotate(${deg}deg)` : 'transform: none';
</script>

<div id="clock-{index}" class="relative bg-blue-500 w-20 h-20 lg:w-32 lg:h-32 rounded-full">
    <!-- {#each [...Array(10).keys()] as i}
        <div class="absolute w-[20px] h-[10%] top-[40%] left-[49%]" style="transform: rotate({i*30}deg)">TES</div>
    {/each} -->
    <div id="needle-{index}" active="{active}" class="w-[4px] lg:w-[8px] h-[40%] bg-black absolute top-[10%] left-[calc(50%-2px)] lg:left-[calc(50%-4px)] origin-bottom transition-all" style="{transform}"></div>
</div>