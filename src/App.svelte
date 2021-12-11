<script>
	import { brands } from './lib/data.js';
	const numbers = {
		group: 0,
		index: 0
	}
	let showAnswer = false
	let quiz = brands[numbers.group][numbers.index]
	const toggle = () => {
		showAnswer = !showAnswer
	}
	const changeIndex = (number) => {
		if (!showAnswer) {
			showAnswer = !showAnswer
		} else if ((numbers.index < brands[numbers.group].length - 1 && number > 0) || (number < 0 && numbers.index > 0)) {
			numbers.index += number
			quiz = brands[numbers.group][numbers.index]
			showAnswer = false
		}
	}
	const changeGroup = (number) => {
		if (!showAnswer) {
			showAnswer = !showAnswer
		} else if ((numbers.group < brands.length - 1 && number > 0) || (number < 0 && numbers.group > 0)) {
			numbers.group += number
			numbers.index = 0
			quiz = brands[numbers.group][numbers.index]
			showAnswer = false
		}
	}
</script>

<svelte:head>
	<title>{numbers.group + 1}组-{numbers.index + 1}题</title>
</svelte:head>
<main style="height: 80%">
	<section style="padding-top: 100px;">
		<img src="{quiz.img}" alt="">
		<div style="height: 64px">
			{#if (showAnswer)}
				<h2>{quiz.answer}</h2>
			{/if}
		</div>
		<div style="margin-bottom: 10px;">
			<button on:click={() => changeIndex(-1)}>上一题</button>
			<button on:click={() => changeIndex(1)}>下一题</button>
		</div>
		<div>
			<button on:click={() => changeGroup(-1)}>上一组</button>
			<button on:click={() => changeGroup(1)}>下一组</button>
		</div>

	</section>
</main>

<footer>
	<p>GoBa<a href="#;">nana</a></p>
</footer>
<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	button {
		padding: .3em .7em;
		border-radius: 4px;
		font-weight: 300;
		color: #444;
		border: 1px solid #444;
	}
	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	footer a {
		font-weight: bold;
		color: #ff3e00;
	}

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
