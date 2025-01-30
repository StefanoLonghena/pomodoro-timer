<script>
	let play = $state(false);
	let seconds = $state(0);
	setInterval(() => {
		if (play) {
			seconds += 1;
		}
	}, 1000);
</script>

<h1>{seconds}</h1>
<button onclick={play ? play=false : play=true}>{play ? "Pause" : "Play"}</button>
