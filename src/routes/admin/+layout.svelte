<script lang="ts">
  import '$lib/app.css'

  import Logo from '$lib/components/Logo.svelte'
</script>

<sveltekit::head>
  <title>Helyettesítés | Admin</title>
</sveltekit::head>

<div class="flex flex-col bg-slate-700 min-h-svh">
  <nav class="dark:text-slate-300 dark:bg-slate-900 p-3 mt-2 mx-2 rounded-2xl shadow-xl">
    <div class="flex items-center justify-between text-lg">
      <div class="flex flex-row items-center gap-1">
        <Logo logoClass="w-10 h-10 dark:invert" />
        <h1 class="font-black">Helyettesítés</h1>
        <span class="text-xs text-slate-500">by PetrikReal</span>
      </div>
    </div>
  </nav>
  <slot />
</div>
