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
		if ((numbers.index < brands[numbers.group].length - 1 && number > 0) || (number < 0 && numbers.index > 0)) {
			numbers.index += number
			quiz = brands[numbers.group][numbers.index]
			showAnswer = false
		}
	}
	const changeGroup = (number) => {
		if ((numbers.group < brands.length - 1 && number > 0) || (number < 0 && numbers.group > 0)) {
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

<section>
	<img src="{quiz.img}" alt="">
	<div style="height: 64px">
		{#if (showAnswer)}
			<h2>{quiz.answer}</h2>
		{/if}
	</div>
	<div style="margin-bottom: 10px;">
		<button on:click={() => changeIndex(-1)}>上一个</button>
		<button on:click={toggle}>显示答案</button>
		<button on:click={() => changeIndex(1)}>下一个</button>
	</div>
	<div>
		<button on:click={() => changeGroup(-1)}>上一组</button>
		<button on:click={() => changeGroup(1)}>下一组</button>
	</div>

</section>

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
</style>
