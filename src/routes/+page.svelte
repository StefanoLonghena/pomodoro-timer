<script>
	import Clock from '$lib/components/Clock.svelte';
	let reset = $state(false);

	function triggerReset() {
		reset = true;
	}

	function resetCallback() {
		reset = false;
	}
</script>

<button onclick={triggerReset} class="hover:cursor-pointer"
aria-label="reset"
	><svg
		xmlns="http://www.w3.org/2000/svg"
		fill="none"
		viewBox="0 0 24 24"
		stroke-width="1.5"
		stroke="currentColor"
		class="size-6"
	>
		<path
			stroke-linecap="round"
			stroke-linejoin="round"
			d="M9 15 3 9m0 0 6-6M3 9h12a6 6 0 0 1 0 12h-3"
		/>
	</svg>
</button>
<div
	class="bg-[#010101] absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 p-10 rounded-2xl w-[50vh] h-[50vh]"
>
	<Clock {reset} {resetCallback} />
</div>
