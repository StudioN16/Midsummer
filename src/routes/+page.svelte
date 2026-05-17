<script>
	import { fly } from 'svelte/transition';
	import { base } from '$app/paths';

	let visible = true;
</script>

<div class="min-h-screen flex flex-col items-center justify-center px-6 relative overflow-hidden">

	<svg class="absolute bottom-0 left-0 pointer-events-none" width="200" height="420" viewBox="0 0 160 340" fill="none">
		<rect x="72" y="260" width="16" height="80" rx="4" fill="#1a0f2e"/>
		<ellipse cx="65" cy="230" rx="38" ry="55" fill="#0d1f10"/>
		<ellipse cx="50" cy="190" rx="30" ry="45" fill="#122518"/>
		<ellipse cx="75" cy="200" rx="35" ry="50" fill="#0d1f10"/>
		<ellipse cx="40" cy="155" rx="25" ry="38" fill="#122518"/>
		<ellipse cx="68" cy="160" rx="30" ry="42" fill="#0d1f10"/>
		<ellipse cx="30" cy="120" rx="22" ry="34" fill="#122518"/>
		<ellipse cx="60" cy="125" rx="26" ry="36" fill="#0d1f10"/>
		<ellipse cx="18" cy="90" rx="18" ry="28" fill="#122518"/>
		<ellipse cx="48" cy="88" rx="22" ry="30" fill="#0d1f10"/>
		<circle cx="85" cy="195" r="2" fill="#9b72cf" opacity="0.5"/>
		<circle cx="42" cy="148" r="1.5" fill="#c4a0f0" opacity="0.4"/>
		<circle cx="20" cy="105" r="1.5" fill="#9b72cf" opacity="0.35"/>
	</svg>

	<svg class="absolute bottom-0 right-0 pointer-events-none" style="transform: scaleX(-1)" width="200" height="420" viewBox="0 0 160 340" fill="none">
		<rect x="72" y="260" width="16" height="80" rx="4" fill="#1a0f2e"/>
		<ellipse cx="65" cy="230" rx="38" ry="55" fill="#0d1f10"/>
		<ellipse cx="50" cy="190" rx="30" ry="45" fill="#122518"/>
		<ellipse cx="75" cy="200" rx="35" ry="50" fill="#0d1f10"/>
		<ellipse cx="40" cy="155" rx="25" ry="38" fill="#122518"/>
		<ellipse cx="68" cy="160" rx="30" ry="42" fill="#0d1f10"/>
		<ellipse cx="30" cy="120" rx="22" ry="34" fill="#122518"/>
		<ellipse cx="60" cy="125" rx="26" ry="36" fill="#0d1f10"/>
		<ellipse cx="18" cy="90" rx="18" ry="28" fill="#122518"/>
		<ellipse cx="48" cy="88" rx="22" ry="30" fill="#0d1f10"/>
		<circle cx="85" cy="195" r="2" fill="#9b72cf" opacity="0.5"/>
		<circle cx="42" cy="148" r="1.5" fill="#c4a0f0" opacity="0.4"/>
		<circle cx="20" cy="105" r="1.5" fill="#9b72cf" opacity="0.35"/>
	</svg>

	<svg class="absolute inset-0 w-full h-full pointer-events-none" viewBox="0 0 600 500" preserveAspectRatio="xMidYMid slice">
		<circle cx="120" cy="60" r="1.5" fill="#9b72cf" opacity="0.6"/>
		<circle cx="480" cy="40" r="1" fill="#c4a0f0" opacity="0.5"/>
		<circle cx="300" cy="30" r="1" fill="#9b72cf" opacity="0.4"/>
		<circle cx="200" cy="80" r="1.5" fill="#c4a0f0" opacity="0.35"/>
		<circle cx="420" cy="70" r="1" fill="#9b72cf" opacity="0.5"/>
		<circle cx="530" cy="100" r="1.5" fill="#c4a0f0" opacity="0.4"/>
		<circle cx="80" cy="120" r="1" fill="#9b72cf" opacity="0.3"/>
		<circle cx="350" cy="55" r="1" fill="#c4a0f0" opacity="0.45"/>
	</svg>

	{#if visible}
		<div class="relative z-10 flex flex-col items-center gap-6 text-center" transition:fly={{ y: 30, duration: 800 }}>
			<p class="text-purple-600 text-xs tracking-widest uppercase">The Play Group Theatre presents</p>
			<h1 class="text-purple-100 text-5xl leading-tight" style="font-family: 'Crimson Text', serif; font-style: italic;">
				A Midsummer<br/>Night's Dream
			</h1>
			<p class="text-purple-700 text-xs tracking-widest">PGT Style</p>

			<div class="flex flex-col gap-3 mt-6 w-full max-w-xs">
<a href="/Midsummer/quotes" class="px-6 py-3 rounded-full border border-purple-800 text-purple-400 hover:bg-purple-950 hover:text-purple-200 transition-all duration-300 text-sm tracking-widest uppercase">
	Quotes
</a>
<a href="/Midsummer/tictactoe" class="px-6 py-3 rounded-full border border-purple-800 text-purple-400 hover:bg-purple-950 hover:text-purple-200 transition-all duration-300 text-sm tracking-widest uppercase">
	Moth Tac Toe
</a>
			</div>
		</div>
	{/if}
</div>