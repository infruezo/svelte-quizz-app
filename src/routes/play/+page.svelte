<script>
  // @ts-nocheck

  import GameBoard from "../../components/GameBoard.svelte";
  import { categories, difficulties, types, numbers } from "../../data/index";

  let selectedQuestionsNumber;
  let selectedCategory;
  let selectedDifficulty;
  let selectedQuestionsType;
  $: showGameBoard = false;
  let promise = Promise.resolve([]);

  async function fetchQuestions(url) {
    let category =
      selectedCategory === "Any" ? "" : `&category=${selectedCategory}`;
    let difficulty =
      selectedDifficulty === "all" ? "" : `&difficulty=${selectedDifficulty}`;
    let type =
      selectedQuestionsType === "All" ? "" : `&type=${selectedQuestionsType}`;
    const response = await fetch(
      `https://opentdb.com/api.php?amount=${selectedQuestionsNumber}${category}${difficulty}${type}`
    );

    if (response.ok) {
      return response.json();
    } else {
      throw new Error("Something went wrong...");
    }
  }

  function handleSubmit() {
    fetchQuestions();
    promise = fetchQuestions();
    showGameBoard = true;
  }
</script>

<div
  class="flex h-full min-h-screen w-full flex-col items-center pt-12 md:pt-24 lg:space-y-9 lg:py-36"
>
  {#if !showGameBoard}
    <form
      action=""
      on:submit={handleSubmit}
      class="flex w-11/12 flex-col space-y-4 rounded-lg bg-white p-10 drop-shadow-xl filter md:w-10/12 lg:w-[400px]"
    >
      <div class="mx-auto flex w-full flex-col space-y-2">
        <label for="questionsNumber" class="text-lg">Number of questions:</label
        >
        <select
          bind:value={selectedQuestionsNumber}
          name="questionsNumber"
          id="questionsNumber"
          class="w-full px-4 py-2 text-sm shadow-md outline-none ring-1 ring-blue-200 selection:ring-blue-400"
        >
          <option value="10" disabled selected>Any (default 10)</option>
          {#each numbers as number}
            <option value={number} id={number}>{number}</option>
          {/each}
        </select>
      </div>

      <div class="flex flex-col space-y-2">
        <label for="category" class="text-lg">Select Category:</label>
        <select
          name="category"
          id="category"
          class="w-full px-4 py-2 text-sm shadow-md outline-none ring-1 ring-blue-200 selection:ring-blue-400"
          bind:value={selectedCategory}
        >
          <option disabled selected value="Any">All Categories</option>
          {#each categories as { id, name }}
            <option value={id} {id}>{name}</option>
          {/each}
        </select>
      </div>

      <div class="flex flex-col space-y-2">
        <label for="difficulty" class="text-lg">Select Difficulty:</label>
        <select
          name="difficulty"
          id="difficulty"
          class="w-full px-4 py-2 text-sm shadow-md outline-none ring-1 ring-blue-200 selection:ring-blue-400"
          bind:value={selectedDifficulty}
        >
          {#each difficulties as difficulty}
            <option value={difficulty.toLowerCase()} id={difficulty}
              >{difficulty}</option
            >
          {/each}
        </select>
      </div>

      <div class="flex flex-col space-y-2">
        <label for="type" class="text-lg">Select Type:</label>
        <select
          name="type"
          id="type"
          class="w-full px-4 py-2 text-sm shadow-md outline-none ring-1 ring-blue-200 selection:ring-blue-400"
          bind:value={selectedQuestionsType}
        >
          {#each types as { name, value }}
            <option {value} id={name}>{name}</option>
          {/each}
        </select>
      </div>

      <div
        class="!mt-8 flex w-full items-center justify-between space-x-3 md:space-x-4 lg:space-x-8"
      >
        <a
          class="flex-1 rounded-md bg-white py-2 text-center text-gray-900 shadow-lg ring-2 ring-gray-900 duration-300 hover:text-pink-500 hover:shadow-xl hover:ring-pink-500"
          href="./"
        >
          Go Back
        </a>
        <button
          type="submit"
          class="flex-1 rounded-md bg-white py-2 text-center text-gray-900 shadow-lg ring-2 ring-gray-900 duration-300 hover:text-blue-500 hover:shadow-xl hover:ring-blue-500"
          >Start Playing
        </button>
      </div>
    </form>
  {:else}
    {#await promise}
      <div
        class="w-full h-full flex items-center justify-center pt-24 md:pt-32 lg:pt-64"
      >
        <img src="./loader.svg" class="h-full w-auto object-cover" alt="" />
      </div>
    {:then value}
      <GameBoard questions={value} />
    {:catch error}
      <p>error</p>
    {/await}
  {/if}
</div>
