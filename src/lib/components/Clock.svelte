<script>
	let play = $state(false);
	let seconds = $state(5);
	let minutes = $derived(seconds / 60);
	let pause = false;
	let fillAngle = $state(0);
	let cycles = $state(0);

	let { reset, resetCallback } = $props();


	setInterval(() => {
		if (play) {
			seconds -= 1;
		}
	}, 1000);

	$effect(() => {
		if (seconds === 0) {
			if (pause) {
				seconds = 25 * 60;
				pause = false;
			} else {
				seconds = 5 * 60;
				cycles++;
				pause = true;
			}
		}

		if(reset) {
			seconds = 25*60;
			cycles = 0;
			resetCallback();
		}

		fillAngle = (1 - seconds / (pause ? 5 * 60 : 25 * 60)) * 360;
	});

</script>

<div class="flex flex-col items-center h-full justify-around">
	<div
		class=" flex flex-col items-center justify-center rounded-full p-[10px] w-[30vh] h-[30vh]"
		style="background: conic-gradient(from 0deg, #EF4444 0deg, #EF4444 {fillAngle -
			15}deg, #1F2937 {fillAngle}deg, #1F2937 360deg)"
	>
		<p
			class="text-[8vh] font-roboto text-center text-[#fdfdfd] tabular-nums bg-[#010101] w-full h-full rounded-full flex items-center justify-center"
		>
			{parseInt(minutes).toString().padStart(2, '0')}:{(seconds % 60).toString().padStart(2, '0')}
		</p>
		<div class="absolute bottom-[20vh] left-1/2 transform -translate-x-1/2 flex">
			<svg onclick={() => { cycles <= 4 ? cycles++ : True }} xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="size-6 text-white">
				<path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
			  </svg>
			{#each { length: 4 }, index}
				{#if index < cycles}
					<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 24 24"
						fill="currentColor"
						class="size-6 text-red-500"
					>
						<path
							fill-rule="evenodd"
							d="M4.5 7.5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-9a3 3 0 0 1-3-3v-9Z"
							clip-rule="evenodd"
						/>
					</svg>
				{:else}
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor"
						class="size-6 text-white"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M5.25 7.5A2.25 2.25 0 0 1 7.5 5.25h9a2.25 2.25 0 0 1 2.25 2.25v9a2.25 2.25 0 0 1-2.25 2.25h-9a2.25 2.25 0 0 1-2.25-2.25v-9Z"
						/>
					</svg>
				{/if}
			{/each}
			<svg onclick={() => { cycles > 0 ? cycles-- : True }} xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="size-6 text-white">
				<path stroke-linecap="round" stroke-linejoin="round" d="M5 12h14" />
			  </svg>
			  
		</div>
	</div>
	<button
		class="px-[4vh] py-[1.5vw] rounded-3xl bg-[#3d3d3d] hover:cursor-pointer"
		onclick={() => (play ? (play = false) : (play = true))}>{play ? 'Pause' : 'Play'}</button
	>
</div>
