<script lang="ts">
	//これをpostする?
	let sampleData = [
		{
			title: 'new',
			counter: 0
		},
		{
			title: 'new',
			counter: 0
		},
		{
			title: 'new',
			counter: 0
		},
	]
	// countの合計値
	function sumCounter(sampleData): number {
		let sum = 0;
		sampleData.forEach(value => {
			sum = sum + value.counter
		})
		return sum;
	}

	$: sumCount = sumCounter(sampleData);

	//counter増やす
	function add(): void {
		sampleData = sampleData.concat({ title: 'new', counter: 0 });
	}
	//counter消す
	function deleteButton(index: number): void {
		const result = sampleData.filter(value => {
			return value != sampleData[index];
		});
		sampleData = result;
	}
</script>

<main>
	<h1>Multiple Counter</h1>

	{#each sampleData as {title, counter}, index (index)}
		<div class="card">
			<!-- inputの部分 -->
			<div class="text-input">
				<input type="text"
					bind:value={title}
					placeholder="new"
				>
			</div>
			<!-- カウント表示部分 -->
			<div class="counter">
				{counter}
			</div>
			<!-- プラスマイナスリセットボタン -->
			<div class="counter-buttons">
				<button on:click={() => counter++}>+</button>
				{#if counter == 0}
					<button disabled on:click={() => counter--}>-</button>
				{:else}
					<button on:click={() => counter--}>-</button>
				{/if}
				<button on:click={() => counter = 0}>0</button>
				<button on:click={() => deleteButton(index)}>x</button>
			</div>
		</div>
	{/each}

	<!-- new counter -->
	<button class="new-counter" on:click={add}>
		new counter
	</button>

	<!-- countの合計値 -->
	<p>
		countの合計値: {sumCount}
	</p>

	<!-- タイトル表示 -->
	<p>タイトルリスト</p>
	<ul>
		{#each sampleData as {title}, index (index)}
			<li style="list-style-type: none;">
				{title}
			</li>
		{/each}
	</ul>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	.card {
		display: flex;
  	    justify-content: space-around;
		align-items: center;
		max-width: 600px;
		height: 60px;
		margin: 0 auto;
		margin-top: 20px;
		box-shadow: 3px 3px 3px 2px rgba(0,0,0,0.6);
	}

	.new-counter {
		margin: 0 auto;
		background-color: green;
		color: white;
		width: 600px;
		margin-top: 20px;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>