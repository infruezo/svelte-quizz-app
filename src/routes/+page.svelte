<svelte:head>
  <title>QuizzU</title>
</svelte:head>

<div
  class="relative flex h-full min-h-screen w-full flex-col items-center space-y-6 pt-24 md:pt-36 lg:space-y-9 lg:pt-48 xl:pt-64"
>
  <p class="absolute bottom-2 text-sm text-gray-400">
    Questions are fetched from
    <a
      href="https://opentdb.com/"
      target="_blank"
      rel="noreferrer"
      class="text-blue-300 underline duration-300 hover:text-pink-500"
    >
      Open Trivia DB
    </a>
  </p>
  <h1 class="text-7xl font-semibold  text-gray-900 drop-shadow-md filter">
    QuizzU
  </h1>

  <div class="flex flex-col space-y-6">
    <a
      href="./play"
      class="rounded-md bg-white py-2 px-6 text-gray-900 shadow-lg ring-2 ring-gray-900 duration-300 hover:text-pink-500 hover:shadow-xl hover:ring-pink-500"
    >
      Start Game
    </a>
    <a
      href="./how-to-play"
      class="rounded-md bg-white py-2 px-6 text-gray-900 shadow-lg ring-2 ring-gray-900 duration-300 hover:text-blue-500 hover:shadow-xl hover:ring-blue-500"
    >
      How To Play
    </a>
  </div>
</div>
