<script lang="ts">
  export let teacher: any[]
</script>

<div class="bg-slate-800 p-1 rounded-xl shadow-xl">
  <table class="sub-table mt-4 w-full text-sm text-left md:table-fixed">
    <caption class="text-lg text-center font-semibold mb-1">{teacher[0].expand.from.name}</caption>
    <thead class="text-xs">
      <tr>
        <th scope="col">Óra</th>
        <th scope="col">Osztály</th>
        <th scope="col">Tanár</th>
        <th scope="col">Terem</th>
        <th scope="col">Megjegyzés</th>
      </tr>
    </thead>
    <tbody>
      {#each teacher as sub}
        <tr>
          <th scope="row" class="font-medium">{sub.period}.</th>
          <td>{sub.expand.class.name}</td>
          {#if !sub.isCancelled}
            <td>{sub.expand.to.name}</td>
            <td>{sub.expand.room.name}</td>
            <td>{sub.comment}</td>
          {:else}
            <td>-</td>
            <td class="font-semibold">Elmarad</td>
            <td>{sub.comment}</td>
          {/if}
        </tr>
      {/each}
    </tbody>
  </table>
</div>
