<script lang="ts">
  import DayDisplay from '$lib/components/day/DayDisplay.svelte';
  import { pb } from '$lib/pocketbase';

  let pbPromise = pb.collection('subsSplit').getFullList();

  import { classFilter } from '$lib/store/classFilter';
</script>

{#await pbPromise}
  <p>Loading...</p>
{:then data}
  <div class="justify-center">
    <div class="max-w-5xl mx-auto">
      {#each data as day}
        {#if $classFilter === '' || day.classes.includes($classFilter)}
          <DayDisplay
            date={day.day}
            teachers={day.teachers}
            specialScheduleLink={day?.schedule}
            comment={day?.comment}
          />
        {/if}
      {/each}
      <!-- check if filtered class has no subs -->
      {#if data.filter((day) => day.classes.includes($classFilter)).length === 0}
        <div class="w-full flex flex-col justify-center items-center">
          <p class="text-center text-xl mt-4 text-slate-300 font-black">Nincs helyettesítés!</p>
          <button
            class="text-center text-slate-700 font-bold p-2 w-36 mt-3 rounded-xl shadow-xl bg-emerald-400"
            on:click={() => {
              classFilter.set('');
            }}>Összes osztály</button
          >
        </div>
      {/if}
    </div>
  </div>
{:catch error}
  <p>{error.message}</p>
{/await}
