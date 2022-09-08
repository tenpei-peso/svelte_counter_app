<script lang="ts">
  let initialCounters = [
    {
      title: 'new',
      counter: 0,
    },
    {
      title: 'new',
      counter: 0,
    },
    {
      title: 'new',
      counter: 0,
    },
  ];

  function sumCounter(
    initialCounters: {
      title: string;
      counter: number;
    }[],
  ): number {
    let sum = 0;
    initialCounters.forEach((value) => {
      sum = sum + value.counter;
    });
    return sum;
  }

  $: sumCount = sumCounter(initialCounters);

  function add(): void {
    initialCounters = initialCounters.concat({ title: 'new', counter: 0 });
  }

  function deleteButton(index: number): void {
    const result = initialCounters.filter((value) => {
      return value != initialCounters[index];
    });
    initialCounters = result;
  }
</script>

<main>
  <h1>Multiple Counter</h1>

  {#each initialCounters as { title, counter }, index (index)}
    <div class="card">
      <div class="text-input">
        <input type="text" bind:value={title} placeholder="new" />
      </div>

      <div class="counter">
        {counter}
      </div>

      <div class="counter-buttons">
        <button on:click={() => counter++}>+</button>
        {#if counter == 0}
          <button disabled on:click={() => counter--}>-</button>
        {:else}
          <button on:click={() => counter--}>-</button>
        {/if}
        <button on:click={() => (counter = 0)}>0</button>
        <button on:click={() => deleteButton(index)}>x</button>
      </div>
    </div>
  {/each}

  <button class="new-counter" on:click={add}> new counter </button>

  <p>
    countの合計値: {sumCount}
  </p>

  <p>タイトルリスト</p>
  <ul>
    {#each initialCounters as { title }, index (index)}
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
    box-shadow: 3px 3px 3px 2px rgba(0, 0, 0, 0.6);
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
