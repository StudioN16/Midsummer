<script>
	import '../app.css';
	import { base } from '$app/paths';
	let { children } = $props();
</script>

<svelte:head>
	<title>A Midsummer Night's Dream</title>
	<meta name="description" content="A Midsummer Night's Dream as heard by a voice memo" />
	<meta name="author" content="StudioN16" />
</svelte:head>

<nav class="fixed top-0 w-full z-50 flex items-center justify-between px-6 py-3">
	<a href="{base}/" class="text-purple-600 text-xs tracking-widest uppercase hover:text-purple-300 transition-colors">Home</a>
	<div class="flex gap-6">
		<a href="{base}/quotes" class="text-purple-600 text-xs tracking-widest uppercase hover:text-purple-300 transition-colors">Quotes</a>
		<a href="{base}/tictactoe" class="text-purple-600 text-xs tracking-widest uppercase hover:text-purple-300 transition-colors">Moth Tac Toe</a>
	</div>
</nav>

{@render children()}