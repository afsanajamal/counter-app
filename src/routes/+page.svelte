<script lang="ts">
  import { setContext } from "svelte";
  import "../app.css";
  import Counter from "../components/Counter.svelte";
  setContext("counter", { removeCounter });
  let counterCount: counterObject[] = [];
  $: allDetails = getAllDetails(counterCount);

  function getAllDetails(counterList: counterObject[]) {
    return {
      titleList: counterList
        .filter((counter) => counter.title !== "")
        .map((counter) => counter.title)
        .join(", "),
      total: counterList.reduce((result, curr) => result + curr.count, 0),
    };
  }

  function createCounter() {
    counterCount = counterCount.length
      ? [
          ...counterCount,
          {
            id: counterCount[counterCount.length - 1].id + 1,
            count: 0,
            title: `counter${counterCount[counterCount.length - 1].id + 1}`,
          },
        ]
      : [
          {
            id: 1,
            count: 0,
            title: "counter-1",
          },
        ];
  }

  function removeCounter(index: number) {
    counterCount = counterCount.filter((counter) => counter.id !== index);
  }
</script>

<section>
  <h1 class="text-4xl text-center my-4">Multiple Counter</h1>
  <div class="relative block w-1/3 mx-auto">
    {#each counterCount as counter}
      <Counter bind:counter />
    {/each}
    <button
      class="w-32 block mx-auto my-4 text-center bg-green-400 rounded text-white cursor-pointer pointer-hover"
      on:click={() => createCounter()}
      aria-label="Create counter"
    >
      New Counter
    </button>
  </div>
  <div class="relative block w-1/3 mx-auto text-center">
    <p>{`Counter list: ${allDetails.titleList}`}</p>
    <p>{`Sum of count: ${allDetails.total}`}</p>
  </div>
</section>
