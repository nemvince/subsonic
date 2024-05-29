<script lang="ts">
  import Icon from '@iconify/svelte';
  import { blur } from 'svelte/transition';
</script>

<div transition:blur={{ duration: 300 }} class="absolute top-0 left-0 h-svh w-svw">
  <div class="flex justify-center text-slate-300 items-center gap-3 flex-col md:flex-row w-svw h-svh bg-slate-800">
    <div class="animate-spin text-4xl">
      <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" {...$$props}>
        <g fill="currentColor">
          <path fill-rule="evenodd" d="M12 19a7 7 0 1 0 0-14a7 7 0 0 0 0 14m0 3c5.523 0 10-4.477 10-10S17.523 2 12 2S2 6.477 2 12s4.477 10 10 10" clip-rule="evenodd" opacity="0.2" />
          <path d="M2 12C2 6.477 6.477 2 12 2v3a7 7 0 0 0-7 7z" />
        </g>
      </svg>
    </div>
    <h1 class="font-semibold text-xl">Betöltés...</h1>
  </div>
</div>