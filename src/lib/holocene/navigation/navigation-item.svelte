<script lang="ts">
  import type { IconName } from '$lib/holocene/icon';
  import { navOpen } from '$lib/stores/nav-open';

  import Icon from '../icon/icon.svelte';

  export let link: string;
  export let label: string;
  export let icon: IconName;
  export let tooltip = label;
  export let external = false;
  export let animate = false;

  $: rel = external ? 'noopener noreferrer' : '';
  $: target = external ? '_blank' : '';
</script>

<div role="listitem" data-testid={$$props['data-testid']} class="relative">
  <a
    href={link}
    {rel}
    {target}
    class="mb-1 flex items-center whitespace-nowrap rounded-lg p-1 pl-2 text-sm font-medium hover:bg-white hover:text-black group-[.surface-primary]:hover:bg-black group-[.surface-primary]:hover:text-white group-[.surface-primary]:dark:hover:bg-white group-[.surface-primary]:dark:hover:text-black"
  >
    <div
      class="flex h-6 w-6 items-center after:absolute after:left-[calc(100%_+_1.5rem)] after:top-0 after:hidden after:h-8 after:items-center after:rounded-md after:bg-slate-800 after:p-1 after:px-2 after:text-xs after:text-white after:content-[attr(data-tooltip)] group-data-[nav=closed]:hover:after:flex"
      data-tooltip={tooltip}
    >
      <Icon name={icon} {animate} />
    </div>
    <div
      class="opacity-0 transition-opacity group-data-[nav=open]:opacity-100"
      class:pointer-events-none={!$navOpen}
    >
      {label}
    </div>
  </a>
</div>
