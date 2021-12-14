<script>
	import { brands, gestures } from './lib/data.js';
	let started = false
	let mode = true
	const numbers = {
		group: 0,
		index: 0
	}
	let showAnswer = false
	let quiz = null
	const groupArr = new Array(8)
	const changeIndex = (number) => {
		const games = mode ? brands : gestures
		if (mode && !showAnswer) {
			showAnswer = !showAnswer
		}else if ((numbers.index < games[numbers.group].length - 1 && number > 0) || (number < 0 && numbers.index > 0)) {
			numbers.index += number
			quiz = games[numbers.group][numbers.index]
			showAnswer = false
		}
	}
	const goToGroup = (number) => {
		started = true
		const games = mode ? brands : gestures
		numbers.group = number - 1
		numbers.index = 0
		quiz = games[numbers.group][numbers.index]
		showAnswer = false
	}
	const changeMode = () => {
		mode = !mode
		started = !started
	}
</script>

<svelte:head>
	<title>大前端游戏</title>
</svelte:head>
<main style="height: 80%">
	<section style="padding-top: 100px;">
		{#if started}
			{#if mode}
				<img height="200px" src="{quiz.img}" alt="">
				<div style="height: 64px">
					{#if (showAnswer)}
						<h2>{quiz.answer}</h2>
					{/if}
				</div>
			{:else}
				<h3>{quiz}</h3>
			{/if}
		<div style="margin-bottom: 10px;">
			<button on:click={() => changeIndex(-1)}>上一题</button>
			<button on:click={() => changeIndex(1)}>下一题</button>
		</div>
		{:else}
			<div style="margin-bottom: 20px"><img height="200px" src="./logos/0.png" alt=""></div>
		{/if}
		<div>
			{#each groupArr as g, i}
				<button style="margin: 0 1px" on:click={() => goToGroup(i + 1)}>{i + 1}</button>
			{/each}
		</div>
		<div style="padding-top: 20px">
			<button style="margin: 0 1px" on:click={changeMode }>{#if mode}猜谜飞镖{:else}你划我猜{/if}</button>
		</div>
	</section>
</main>
<footer>
	<p>GoBa<a href="#;">nana</a></p>
</footer>
<style>
	h2 {
		font-size: 22px;
		font-weight: normal;
	}
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
