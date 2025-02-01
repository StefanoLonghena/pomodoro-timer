<script>
	let play = $state(false);
	let seconds = $state(2);
	let minutes = $derived(seconds / 60);
	let pause = false;
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
	})

	
</script>

<div class="flex flex-col items-center">
	<p class="text-[20vw] font-mono">
		{minutes >= 1 ? parseInt(minutes).toString().padStart(2, '0') + ':' : ''}{(seconds % 60)
			.toString()
			.padStart(2, '0')}
	</p>
	<button
		class="px-[15%] py-[5%] rounded-3xl {play ? 'bg-red-500' : 'bg-green-500'} hover:cursor-pointer hover:shadow-2xl"
		onclick={() => (play ? (play = false) : (play = true))}>{play ? 'Pause' : 'Play'}</button
	>
</div>
