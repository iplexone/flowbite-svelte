<script lang="ts">
  import { setContext } from "svelte";
  import { pagination, PaginationItem } from ".";
  import type { PaginationProps } from "$lib/types";
  import { getTheme } from "$lib/theme/themeUtils";
  import clsx from "clsx";

  let { pages = [], previous, next, prevContent, nextContent, table, size, ariaLabel, ...restProps }: PaginationProps = $props();

  const theme = getTheme("pagination");

  setContext("group", true);
  setContext("table", table);
  setContext("size", size);

  const paginationCls = $derived(pagination({ table, size, class: clsx(theme) }));
</script>

<nav aria-label={ariaLabel}>
  <ul class={paginationCls}>
    {#if typeof previous === "function"}
      <li {...restProps}>
        <PaginationItem {size} onclick={() => previous()} class={table ? "rounded-none rounded-l" : "rounded-none  rounded-s-lg"}>
          {#if prevContent}
            {@render prevContent()}
          {:else}
            Previous
          {/if}
        </PaginationItem>
      </li>
    {/if}
    {#each pages as { name, href, active, size }}
      <li {...restProps}>
        <PaginationItem {size} {active} {href}>
          {name}
        </PaginationItem>
      </li>
    {/each}
    {#if typeof next === "function"}
      <li {...restProps}>
        <PaginationItem {size} onclick={() => next()} class={table ? "rounded-none rounded-r" : "rounded-none rounded-e-lg"}>
          {#if nextContent}
            {@render nextContent()}
          {:else}
            Next
          {/if}
        </PaginationItem>
      </li>
    {/if}
  </ul>
</nav>

<!--
@component
[Go to docs](https://flowbite-svelte.com/)
## Type
[PaginationProps](https://github.com/themesberg/flowbite-svelte/blob/main/src/lib/types.ts#L1166)
## Props
@prop pages = []
@prop previous
@prop next
@prop prevContent
@prop nextContent
@prop table
@prop size
@prop ariaLabel
@prop ...restProps
-->
