<script lang="ts">
  export let error: Error;

  import Icon from '@iconify/svelte';
  import { fade } from 'svelte/transition';
</script>

<div transition:fade={{ duration: 300 }} class="absolute top-0 left-0 h-svh w-svw">
  <div class="flex justify-center text-slate-300 items-center gap-3 flex-col md:flex-row w-svw h-svh bg-slate-800">
    <div class="text-4xl">
      <Icon icon="mingcute:sad-fill" />
    </div>
    <div class="flex flex-col text-center gap-2">
      <h1 class="font-semibold text-xl">Valami nem jó...</h1>
      <p class="text-center text-slate-400">{error.message}</p>
    </div>
  </div>
</div>