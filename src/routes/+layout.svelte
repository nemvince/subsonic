<script lang="ts">
  import '../app.css';

  import Logo from '$lib/components/Logo.svelte';
  import { pb } from '$lib/pocketbase';
  import { classFilter } from '$lib/store/classFilter';

  let selectedClass: string;

  $: classFilter.set(selectedClass);
  $: selectedClass = $classFilter;

  const classesPromise = pb.collection('class').getFullList();
</script>

<div class="flex flex-col bg-slate-700 min-h-svh">
  <nav class="dark:text-slate-300 dark:bg-slate-900 p-3 mt-2 mx-2 rounded-2xl shadow-xl">
    <div class="flex items-center justify-between text-lg gap-2">
      <div class="flex flex-row gap-3">
        <Logo logoClass="w-10 h-10 dark:invert" />
        {#await classesPromise}
          Loading...
        {:then classes}
          <select
            bind:value={selectedClass}
            class="block p-1.5 px-2 text-sm border rounded-lg border-slate-700 bg-slate-900 placeholder-slate-400"
          >
            <option selected value="">Osztály</option>
            {#each classes as classOption}
              <option value={classOption.id}>{classOption.name}</option>
            {/each}
          </select>
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
  <slot {selectedClass} />
</div>
