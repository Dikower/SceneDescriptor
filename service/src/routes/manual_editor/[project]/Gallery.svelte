<script lang="ts">
  import {onMount} from "svelte";
  import {CUTTER_URL} from "$lib/constants";
  import {goto} from '$app/navigation'
  import ProjectCard from "$lib/components/ProjectCard.svelte";

  let projects: unknown[] = []

  onMount(async () => {
    projects = await fetch(new URL('/get_all_projects', CUTTER_URL)).then(r => r.json())
  })
</script>

<div class="border border-gray-800 p-3 rounded-lg flex flex-col max-w-[260px] max-h-[580px]">
  <p class="text-md text-gray-400 font-bold mb-2">Галерея проектов</p>
  <div class="flex flex-col items-center overflow-y-auto" style="scrollbar-width: thin;">
    {#each projects as project}
      <ProjectCard {...project} textCls="text-sm"/>
    {/each}
  </div>
</div>

