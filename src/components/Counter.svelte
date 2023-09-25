<script lang="ts">
  import { getContext } from "svelte";
  export let counter: counterObject;
  const { removeCounter }: any = getContext("counter");
</script>

<div
  class="max-w-lg flex border-solid border-2 bg-gray-100 shadow-lg hover:border-4 rounded mx-auto my-2"
>
  <input
    class="w-3/6 text-gray-600 mx-4 my-2 px-1 w-32"
    data-v-6a69534f=""
    on:input={e => {
      counter.title = e.currentTarget.value;
    }}
    value={counter.title}
  />
  <div class="w-1/6 my-auto mx-auto text-3xl text-bold">
    {counter.count}
  </div>
  <div class="w-2/6 block mx-auto cursor-hover py-2">
    <button
      class="btn bg-red-500 text-2xl w-8 rounded-l pointer-hover"
      tabindex="-1"
      data-v-6a69534f=""
      on:click={() => (counter.count += 1)}>+</button
    >
    <button
      class="btn bg-blue-500 text-2xl w-8 pointer-hover"
      tabindex="-1"
      data-v-6a69534f=""
      on:click={() => (counter.count -= counter.count > 0 ? 1 : 0)}>-</button
    >
    <button
      class="btn bg-yellow-500 text-2xl w-8 rounded-r pointer-hover"
      tabindex="-1"
      data-v-6a69534f=""
      on:click={() => (counter.count = 0)}>0</button
    >
  </div>
  <button
    class="w-8 btn bg-red-500 w-16 ml-1 rounded-r pointer-hover text-white"
    on:click={() => removeCounter(counter.id)}
    aria-label="Increase the counter by one"
  >
    &#9747;
  </button>
</div>
