<script>
	import Clock from '../components/clock.svelte';
	let deg = 0;
	let active = true;
	let intervalPlus;
	let intervalMinus;

	let pin = [true, true, true, true];
	let reel = [
		{ no: 1, pin: 0, clock: 1 },
		{ no: 2, pin: 1, clock: 3 },
		{ no: 3, pin: 2, clock: 7 },
		{ no: 4, pin: 3, clock: 9 }
	];
    
	let clock = [
		{ no: 1, active: true, pin: [0], deg: 0 },
		{ no: 2, active: true, pin: [0, 1], deg: 0 },
		{ no: 3, active: true, pin: [1], deg: 0 },
		{ no: 4, active: true, pin: [0, 2], deg: 0 },
		{ no: 5, active: true, pin: [0, 1, 2, 3], deg: 0 },
		{ no: 6, active: true, pin: [1, 3], deg: 0 },
		{ no: 7, active: true, pin: [2], deg: 0 },
		{ no: 8, active: true, pin: [2, 3], deg: 0 },
		{ no: 9, active: true, pin: [3], deg: 0 }
	];

	function degPlus(pinIndex) {
		disableAllClock();
		let pinState = pin[pinIndex];

		//deg += 30;
		intervalPlus = setInterval(() => {
			if(pinState) {
				let arrDegChanged = [];
				pin.forEach((p, i) => {
					if(p) {
						clock.forEach((c) => {
							if(c.pin.includes(i) && !arrDegChanged.includes(c.no)) {
								c.active = true;
								c.deg += 30;
								arrDegChanged.push(c.no);
							}
						});
					}
				});
			} else {
				reel.forEach((r) => {
					if(r.pin == pinIndex) {
						clock.forEach((c) => {
							if(c.no == r.clock) {
								c.active = true;
								c.deg += 30;
							}
						});
					}
				});
			}
			clock = [...clock];
		}, 100);
	}

	function degMinus(pinIndex) {
		disableAllClock();
		let pinState = pin[pinIndex];

		//deg -= 30;
		intervalPlus = setInterval(() => {
			if(pinState) {
				let arrDegChanged = [];
				pin.forEach((p, i) => {
					if(p) {
						clock.forEach((c) => {
							if(c.pin.includes(i) && !arrDegChanged.includes(c.no)) {
								c.active = true;
								c.deg -= 30;
								arrDegChanged.push(c.no);
							}
						});
					}
				});
			} else {
				reel.forEach((r) => {
					if(r.pin == pinIndex) {
						clock.forEach((c) => {
							if(c.no == r.clock) {
								c.active = true;
								c.deg -= 30;
							}
						});
					}
				});
			}
	
			clock = [...clock];
		}, 100);
	}

	function changePinState(index, state) {
		pin[index] = !state;
	}

	function disableAllClock() {
		clock.forEach((c) => {
			c.active = false;
		});
		clock = [...clock];
	}
</script>

<section class="w-screen h-screen bg-teal-200 flex place-items-center justify-center">
	<div class="fixed top-0 w-screen h-screen grid grid-cols-2 content-between">
		<div class="flex justify-center">
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degMinus(0)}
				on:mouseup={() => clearInterval(intervalMinus)}
				on:touchstart={() => degMinus(0)}
				on:touchend={() => clearInterval(intervalMinus)}>&lt;=</button
			>
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degPlus(0)}
				on:mouseup={() => clearInterval(intervalPlus)}
				on:touchstart={() => degPlus(0)}
				on:touchend={() => clearInterval(intervalPlus)}>=&gt;</button
			>
		</div>
		<div class="flex justify-center">
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degMinus(1)}
				on:mouseup={() => clearInterval(intervalMinus)}
				on:touchstart={() => degMinus(1)}
				on:touchend={() => clearInterval(intervalMinus)}>&lt;=</button
			>
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degPlus(1)}
				on:mouseup={() => clearInterval(intervalPlus)}
				on:touchstart={() => degPlus(1)}
				on:touchend={() => clearInterval(intervalPlus)}>=&gt;</button
			>
		</div>
		<div class="flex justify-center">
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degMinus(2)}
				on:mouseup={() => clearInterval(intervalMinus)}
				on:touchstart={() => degMinus(2)}
				on:touchend={() => clearInterval(intervalMinus)}>&lt;=</button
			>
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degPlus(2)}
				on:mouseup={() => clearInterval(intervalPlus)}
				on:touchstart={() => degPlus(2)}
				on:touchend={() => clearInterval(intervalPlus)}>=&gt;</button
			>
		</div>
		<div class="flex justify-center">
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degMinus(3)}
				on:mouseup={() => clearInterval(intervalMinus)}
				on:touchstart={() => degMinus(3)}
				on:touchend={() => clearInterval(intervalMinus)}>&lt;=</button
			>
			<button
				class="mx-4 my-10 px-2 py-1 bg-green-500 rounded-lg"
				on:mousedown={() => degPlus(3)}
				on:mouseup={() => clearInterval(intervalPlus)}
				on:touchstart={() => degPlus(3)}
				on:touchend={() => clearInterval(intervalPlus)}>=&gt;</button
			>
		</div>
	</div>

	<div class="fixed flex place-items-center">
		<div class="grid grid-cols-2 gap-24 lg:gap-32">
			{#each pin as p, i}
				<button
					class="w-6 h-6 rounded-full z-[1000]"
					style="background: {p ? 'green' : 'red'}"
					on:click={changePinState(i, p)}
				/>
			{/each}
		</div>
	</div>

	<div class="grid grid-cols-3 gap-10">
		{#each clock as c}
			<Clock index={c.no} deg={c.deg} active={c.active} />
		{/each}
	</div>
</section>
