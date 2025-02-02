<script>
	let play = $state(false);
	let seconds = $state(25*60);
	let minutes = $derived(seconds / 60);
	let pause = false;
	let progress = $state(0)
	let fillAngle = $state(0)
	setInterval(() => {
		if (play) {
			seconds -= 1;
		}
	}, 1000);

	$effect(() => {
		if(seconds===0) {
			if(pause) {
				seconds=25*60
				pause=false;
			} else {
				seconds=5*60
				pause=true;
			}
		}

		progress = ((seconds / (pause ? 5*60 : 25*60)));
		fillAngle = (1 - progress) * 360
		console.log(progress)
	})

	
</script>

<div class="flex flex-col items-center h-full justify-around">
	<div class=" flex flex-col items-center justify-center rounded-full p-[10px] w-[30vh] h-[30vh]" style="background: conic-gradient(from 0deg, #EF4444 0deg, #EF4444 {fillAngle}deg, #1F2937 {fillAngle}deg, #1F2937 360deg)">
		<p class="text-[8vh] font-roboto text-center text-[#fdfdfd] tabular-nums bg-[#010101] w-full h-full rounded-full flex items-center justify-center">
			{parseInt(minutes).toString().padStart(2, '0')}:{(seconds % 60)
				.toString()
				.padStart(2, '0')}
		</p>
	</div>
		<button
			class="px-[4vh] py-[1.5vw] rounded-3xl bg-[#3d3d3d] hover:cursor-pointer"
			onclick={() => (play ? (play = false) : (play = true))}>{play ? 'Pause' : 'Play'}</button
		>
</div>
