<script>
	import '../app.css';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';
	let { children } = $props();
	import { onMount } from 'svelte';
	let konamiCode = [38, 38, 40, 40, 37, 39, 37, 39, 66, 65];
	let konamiIndex = 0;

	function handleKeydown(event) {
		if (event.keyCode === konamiCode[konamiIndex]) {
			konamiIndex++;
			if (konamiIndex === konamiCode.length) {
				triggerKonamiEffect();
				konamiIndex = 0;
			}
		} else {
			konamiIndex = 0;
		}
	}

	function triggerKonamiEffect() {
		goto('/konami');
	}

	// Add event listener on mount
	onMount(() => {
		document.addEventListener('keydown', handleKeydown);
		return () => {
			document.removeEventListener('keydown', handleKeydown);
		};
	});
	function url_for(path) {
		const baseUrl = $page.url.origin;
		const url = new URL(path, baseUrl);
		return url.href;
	}
	let homeURL = url_for('/');
	let aboutURL = url_for('/about');
	let factsURL = url_for('/facts');
	let showNavBar = $state(false);
	function mouseHover() {
		showNavBar = true;
	}
	function mouseUnHover() {
		showNavBar = false;
	}
</script>

<svelte:head>
	<title>Midsummer Transcript Quotes</title>
	<meta name="description" content="a website with random midsummer transcript quotes" />
	<meta name="keywords" content="quotes, midsummer, transcript" />
	<meta name="author" content="StudioN16" />
</svelte:head>

{@render children()}
