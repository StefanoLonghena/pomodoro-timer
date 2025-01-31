<script>
	let play = $state(false);
	let seconds = $state(1500);
	let minutes = $derived(seconds/60)
	setInterval(() => {
		if (play) {
			seconds -= 1;
		}
	}, 1000);
</script>

<p class="text-3xl">{minutes >= 1 ? parseInt(minutes).toString().padStart(2, "0") + ":" : ""}{(seconds%60).toString().padStart(2, "0")}</p>
<button class="px-5 py-1 rounded-2xl {play ? "bg-red-500" : "bg-green-500"}" onclick={() => play ? play=false : play=true}>{play ? "Pause" : "Play"}</button>
