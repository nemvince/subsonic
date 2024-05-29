<script lang="ts">
  import '$lib/app.css'

  import Logo from '$lib/components/Logo.svelte'
  import { pb } from '$lib/pocketbase'
  import { classFilter } from '$lib/store/classFilter'
  import { fade, slide } from 'svelte/transition'

  let selectedClass: string
  let className: string

  $: console.log(className)

  $: classFilter.set(selectedClass)
  $: selectedClass = $classFilter
  
  const classesPromise = pb.collection('class').getFullList()
</script>
<sveltekit::head>
  {#if selectedClass}
  <title>Helyettesítés | {selectedClass}</title>
  {:else}
  <title>Helyettesítés</title>
  {/if}
</sveltekit::head>

<div class="flex flex-col bg-slate-700 min-h-svh">
  <nav class="dark:text-slate-300 dark:bg-slate-900 p-3 mt-2 mx-2 rounded-2xl shadow-xl">
    <div class="flex items-center justify-between text-lg gap-2">
      <div class="flex flex-row gap-3 items-center">
        <Logo logoClass="w-10 h-10 dark:invert" />
        {#await classesPromise}
        <div class="animate-spin h-[1em]" transition:slide>
          <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" {...$$props}>
            <g fill="currentColor">
              <path fill-rule="evenodd" d="M12 19a7 7 0 1 0 0-14a7 7 0 0 0 0 14m0 3c5.523 0 10-4.477 10-10S17.523 2 12 2S2 6.477 2 12s4.477 10 10 10" clip-rule="evenodd" opacity="0.2" />
              <path d="M2 12C2 6.477 6.477 2 12 2v3a7 7 0 0 0-7 7z" />
            </g>
          </svg>
        </div>
        {:then classes}
        <div class="" transition:fade={{ delay: 400 }}>
          <select bind:value={selectedClass} class="block p-1.5 px-2 text-sm border rounded-lg border-slate-700 bg-slate-900 placeholder-slate-400">
            <option selected value="">Osztály</option>
            {#each classes as classOption}
            <option value={classOption.id}>{classOption.name}</option>
            {/each}
          </select>
        </div>
        {:catch error}
          <p>{error.message}</p>
        {/await}
      </div>

      <div class="flex flex-col">
        <h1 class="font-black">Helyettesítés</h1>
        <span class="text-xs text-right text-slate-500">by PetrikReal</span>
      </div>
    </div>
  </nav>
  <slot />
</div>
