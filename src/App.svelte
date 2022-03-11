<script>
	// import Guess from './Guess.svelte';
	import { words } from './five-letter-words';

	let input = '';
	let guesses = ['CRANE'];

	const handleKeyPress = (e) => {
		console.log('input', input);
		const { keyCode } = e;

		console.log('keyCode', keyCode);

		if (keyCode === 32) e.preventDefault();

		if (keyCode === 13 && input.length === 5) {
			addGuess();
			clearInput();
		}
	};

	const clearInput = () => {
		input = '';
	};

	const addGuess = () => {
		guesses = [...guesses, input];
	};

	const onClear = () => {
		guesses = [];
	};
</script>

<main>
	<h1>Wordle Guess Getter</h1>
	<p>Enter your guesses and see the most likely words.</p>

	<section class="content">
		<div class="content-left">
			<input
				type="text"
				id="input"
				bind:value={input}
				on:keypress={handleKeyPress}
				maxlength="5"
				tabindex="1"
			/>
			{#if guesses.length > 0}
				<button class="clear-btn" on:click={onClear}>Clear</button>
			{/if}
			{#each guesses as guess}
				<span class="guess"
					>{#each guess as letter}<span class="letter">{letter}</span
						>{/each}</span
				>
			{/each}
		</div>
		<div class="content-right">
			{#each words as word}
				<span class="word">
					{word}
				</span>
			{/each}
		</div>
	</section>
</main>

<style>
	h1 {
		margin-bottom: 0;
	}

	.content {
		display: flex;
	}

	.content-left,
	.content-right {
		flex: 1;
	}

	.content-right {
	}

	.content-left {
		position: relative;
	}

	.guess {
		display: block;
		font-size: 28px;
		text-transform: uppercase;
		font-weight: 700;
	}

	.letter {
		border: 1px solid #ccc;
		display: inline-block;
		height: 2em;
		width: 2em;
		margin-right: 0.5em;
		margin-bottom: 0.5em;
		line-height: 2em;
		text-align: center;
	}

	.word {
		display: block;
		font-size: 24px;
		margin-left: 2em;
	}

	input {
		font-size: 24px;
		margin: 1em 0;
		text-transform: uppercase;
	}

	.clear-btn {
		position: absolute;
		top: 1.8em;
		right: 0;
	}
</style>
