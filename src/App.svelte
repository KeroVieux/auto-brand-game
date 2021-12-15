<script>
	import { brands, gestures } from './lib/data.js';
	let started = false
	let mode = 0
	let showAnswer = false
	let numbers = null
	let games = null
	let quiz = null
	let title = null
	let groupArr = null
	const titles = ['猜谜飞镖','你划我猜','快乐传真']
	const init = () => {
		title = titles[mode]
		numbers = {
			group: 0,
			index: 0
		}
		games = mode ? gestures : brands
		if (mode < 2) {
			quiz = games[numbers.group][numbers.index]
			groupArr = new Array(8)
		} else {
			numbers.group = 8
			numbers.index = 0
			quiz = games[numbers.group][numbers.index]
		}

	}
	init()
	const changeIndex = (number) => {
		const games = mode ? gestures : brands
		if (!mode && !showAnswer) {
			showAnswer = !showAnswer
		}else if ((numbers.index < games[numbers.group].length - 1 && number > 0) || (number < 0 && numbers.index > 0)) {
			numbers.index += number
			quiz = games[numbers.group][numbers.index]
			showAnswer = false
		}
	}
	const goToGroup = (number) => {
		started = true
		if (mode < 2) {
			numbers.group = number - 1
			numbers.index = 0
			quiz = games[numbers.group][numbers.index]
			showAnswer = false
		} else {
			numbers.group = 2
			numbers.index = 0
			quiz = games[numbers.group][numbers.index]
		}

	}
	const changeMode = (number) => {
		mode = number
		started = true
		init()
	}
</script>

<svelte:head>
	<title>大前端游戏</title>
</svelte:head>
<main style="height: 80%">
	<div style="padding-top: 20px">
		<button style="margin: 0 1px" on:click={ () => changeMode(0) }>{titles[0]}</button>
		<button style="margin: 0 1px" on:click={ () => changeMode(1) }>{titles[1]}</button>
		<button style="margin: 0 1px" on:click={ () => changeMode(2) }>{titles[2]}</button>
	</div>
	<section style="padding-top: 80px;">
		{#if started}
			<h1>{title}</h1>
			{#if !mode}
				<img height="200px" src="{quiz.img}" alt="">
				<div style="height: 64px">
					{#if (showAnswer)}
						<h2>{quiz.answer}</h2>
					{/if}
				</div>
			{:else}
				<div style="padding: 40px 0">
					<h3 style="font-size: 52px">{quiz}</h3>
				</div>
			{/if}
		<div style="margin-bottom: 10px;">
			<button on:click={() => changeIndex(-1)}>上一题</button>
			<button on:click={() => changeIndex(1)}>下一题</button>
		</div>
		{:else}
			<div style="margin-bottom: 20px"><img height="400px" src="./logos/cover.jpg" alt=""></div>
		{/if}
		{#if started && mode < 2}
		<div>
			{#each groupArr as g, i}
				<button style="margin: 0 1px" on:click={() => goToGroup(i + 1)}>{i + 1}</button>
			{/each}
		</div>
		{/if}
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
