<script>
	let mode = null; // 'human' or 'computer'
	let board = Array(9).fill(null);
	let currentPlayer = 1;
	let winner = null;
	let computerThinking = false;

	const winningCombos = [
		[0,1,2],[3,4,5],[6,7,8],
		[0,3,6],[1,4,7],[2,5,8],
		[0,4,8],[2,4,6]
	];

	function checkWinner(b) {
		for (const [a, c, d] of winningCombos) {
			if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
		}
		return b.every(Boolean) ? 'draw' : null;
	}

	function computerMove(b) {
		// Try to win
		for (let i = 0; i < 9; i++) {
			if (!b[i]) {
				const test = [...b];
				test[i] = 2;
				if (checkWinner(test) === 2) return i;
			}
		}
		// Try to block
		for (let i = 0; i < 9; i++) {
			if (!b[i]) {
				const test = [...b];
				test[i] = 1;
				if (checkWinner(test) === 1) return i;
			}
		}
		// Take center
		if (!b[4]) return 4;
		// Take a corner
		const corners = [0, 2, 6, 8].filter(i => !b[i]);
		if (corners.length) return corners[Math.floor(Math.random() * corners.length)];
		// Take any
		const available = b.map((v, i) => v ? null : i).filter(v => v !== null);
		return available[Math.floor(Math.random() * available.length)];
	}

	function handleClick(i) {
		if (board[i] || winner || computerThinking) return;
		board[i] = currentPlayer;
		board = [...board];
		winner = checkWinner(board);
		if (!winner) {
			currentPlayer = currentPlayer === 1 ? 2 : 1;
			if (mode === 'computer' && currentPlayer === 2 && !winner) {
				computerThinking = true;
				setTimeout(() => {
					const move = computerMove(board);
					if (move !== undefined) {
						board[move] = 2;
						board = [...board];
						winner = checkWinner(board);
						if (!winner) currentPlayer = 1;
					}
					computerThinking = false;
				}, 500);
			}
		}
	}

	function reset() {
		board = Array(9).fill(null);
		currentPlayer = 1;
		winner = null;
		computerThinking = false;
		mode = null;
	}
</script>

<div class="min-h-screen flex flex-col items-center justify-center gap-8 px-6 relative overflow-hidden" style="background: #0f0c1a;">

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
	</svg>

	<p class="text-purple-600 text-xs tracking-widest uppercase relative z-10">A Midsummer Night's Dream</p>

	{#if !mode}
		<div class="relative z-10 flex flex-col items-center gap-4 text-center">
			<p class="text-purple-300 text-lg italic">how wouldst thou play?</p>
			<button
				onclick={() => mode = 'human'}
				class="px-6 py-2 rounded-full border border-purple-800 text-purple-400 hover:bg-purple-950 hover:text-purple-200 transition-all duration-300 text-sm tracking-widest uppercase"
			>
				two players
			</button>
			<button
				onclick={() => mode = 'computer'}
				class="px-6 py-2 rounded-full border border-purple-800 text-purple-400 hover:bg-purple-950 hover:text-purple-200 transition-all duration-300 text-sm tracking-widest uppercase"
			>
				vs computer
			</button>
		</div>
	{:else}
		<div class="relative z-10 grid grid-cols-3 gap-2">
			{#each board as cell, i}
				<button
					onclick={() => handleClick(i)}
					class="w-28 h-28 rounded-xl overflow-hidden border-2 border-purple-900 hover:border-purple-600 transition-all duration-200"
				>
					{#if cell === null}
						<img src="/moth.webp" alt="moth" class="w-full h-full object-cover opacity-60 hover:opacity-100 transition-opacity"/>
					{:else if cell === 1}
						<img src="/player1.png" alt="player 1" class="w-full h-full object-cover object-top"/>
					{:else}
						<img src="/player2.png" alt="player 2" class="w-full h-full object-cover object-top"/>
					{/if}
				</button>
			{/each}
		</div>

		<div class="relative z-10 text-center flex flex-col items-center gap-3">
			{#if winner === 'draw'}
				<p class="text-purple-300 text-lg italic">a draw... how shakespearean</p>
			{:else if winner}
				<p class="text-purple-300 text-lg italic">
					{winner === 1 ? 'Daniel is The Moth' : 'Vicky is The Moth'}
				</p>
			{:else if computerThinking}
				<p class="text-purple-600 text-xs tracking-widest uppercase">the computer ponders...</p>
			{:else}
				<p class="text-purple-600 text-xs tracking-widest uppercase">
					{currentPlayer === 1 ? 'player one' : mode === 'computer' ? 'computer' : 'player two'}'s turn
				</p>
			{/if}

			<button
				onclick={reset}
				class="px-6 py-2 rounded-full border border-purple-800 text-purple-500 hover:bg-purple-950 hover:text-purple-200 transition-all duration-300 text-sm tracking-wide"
			>
				reset
			</button>
		</div>
	{/if}
</div>

<div class="min-h-screen flex flex-col items-center justify-center gap-8 px-6 relative overflow-hidden" style="background: #0f0c1a;">

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
	</svg>

	<p class="text-purple-600 text-xs tracking-widest uppercase relative z-10">A Midsummer Night's Dream</p>

	<div class="relative z-10 grid grid-cols-3 gap-2">
		{#each board as cell, i}
			<button
				onclick={() => handleClick(i)}
				class="w-28 h-28 rounded-xl overflow-hidden border-2 border-purple-900 hover:border-purple-600 transition-all duration-200"
			>
				{#if cell === null}
					<img src="moth.webp" alt="moth" class="w-full h-full object-cover opacity-60 hover:opacity-100 transition-opacity"/>
				{:else if cell === 1}
					<img src="player1.png" alt="player 1" class="w-full h-full object-cover object-top"/>
				{:else}
					<img src="/player2.png" alt="player 2" class="w-full h-full object-cover object-top"/>
				{/if}
			</button>
		{/each}
	</div>

	<div class="relative z-10 text-center flex flex-col items-center gap-3">
		{#if winner === 'draw'}
			<p class="text-purple-300 text-lg italic">a draw... how shakespearean</p>
		{:else if winner}
			<p class="text-purple-300 text-lg italic">
				{winner === 1 ? 'Vicky is The Moth!' : 'Daniel is The Moth!'}
			</p>
		{:else}
			<p class="text-purple-600 text-xs tracking-widest uppercase">
				{currentPlayer === 1 ? 'player one' : 'player two'}'s turn
			</p>
		{/if}

		<button
			onclick={reset}
			class="px-6 py-2 rounded-full border border-purple-800 text-purple-500 hover:bg-purple-950 hover:text-purple-200 transition-all duration-300 text-sm tracking-wide"
		>
			reset
		</button>
	</div>
</div>