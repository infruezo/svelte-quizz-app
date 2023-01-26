<script>
  // @ts-nocheck
  export let questions;
  $: list = [];

  function setAnswersList(correct_answer, incorrect_answers) {
    list = [];
    list.push(correct_answer);
    incorrect_answers.forEach((element) => {
      list.push(element);
    });

    console.log(list);
  }
</script>

<div
  class="flex h-full w-full flex-col justify-center pt-12 md:pt-24 lg:space-y-9 lg:pt-28"
>
  <div
    class="mx-auto w-11/12 rounded-lg bg-white p-5 drop-shadow-lg filter md:w-10/12 md:p-7 lg:w-[600px] lg:p-10"
  >
    {#each Object.entries(questions) as [response_code, results]}
      {#each Object.entries(results) as [number, { question, correct_answer, incorrect_answers }]}
        <div class="flex items-center justify-between">
          <h3>Question {number}</h3>
          <h3 class="font-medium">
            Score: <span class="font-bold text-green-500">0</span>
          </h3>
        </div>
        <div class="my-8 bg-gray-800 p-3 text-white">
          <p class="font-medium">Q: {@html question}</p>
          <p
            class="cursor-pointer text-gray-800 duration-200 hover:text-emerald-500"
          >
            {correct_answer}
          </p>
        </div>
      {/each}
    {/each}
  </div>
</div>
