<script lang="ts">
  import SubTable from '$lib/components/day/SubTable.svelte'
  import { pb } from '$lib/pocketbase'
  import type { RecordModel } from 'pocketbase'
  import LoadingView from '$lib/views/LoadingView.svelte'

  export let date: Date
  export let specialScheduleLink: string = ''
  export let comment: string = ''
  export let teachers: string
  const subsList = teachers.split(',').filter((sub: string) => sub !== '')

  let promises: Promise<RecordModel[]>[] = []

  subsList.forEach((sub: string) => {
    promises.push(pb.collection('substitution').getFullList({ filter: "from='" + sub + "'", expand: 'from,to,class,room' }))
  })

  import { classFilter } from '$lib/store/classFilter'
</script>

<article class="bg-slate-900 text-slate-300 p-2 mx-2 rounded-xl shadow-lg">
  <div class="w-full pt-3 text-xl font-semibold pl-1">
    <div class="flex flex-row justify-between items-center pr-3">
      <h1>
        {new Date(date).toLocaleDateString('hu-HU', {
          year: 'numeric',
          weekday: 'long',
          month: 'short',
          day: 'numeric'
        })}
      </h1>
      {#if specialScheduleLink !== ''}
        <p class="mt-1 text-sm font-normal text-slate-400">
          <a href={specialScheduleLink} class="underline font-semibold text-emerald-400">
            <p class="hidden md:block">Speciális program</p>
            <p class="block md:hidden">Program</p>
          </a>
        </p>
      {/if}
    </div>

    {#if comment !== ''}
      <p class="mt-1 text-sm font-normal text-slate-400">{comment}</p>
    {/if}
  </div>
  <div class="mt-4 flex flex-col gap-2">
    {#each promises as promise}
      {#await promise}
        <LoadingView />
      {:then teacher}
        {#if teacher.length > 0}
          {#if $classFilter === '' || teacher.some((sub) => sub.class === $classFilter)}
            <SubTable {teacher} />
          {/if}
        {/if}
      {:catch error}
        <p>{error.message}</p>
      {/await}
    {/each}
  </div>
</article>
