<script lang="ts">
  import clsx from "clsx";
  import { TableBodyRow, TableBodyCell } from ".";
  import type { TableBodyProps, CellValue, BodyRow } from "$lib/types";
  import { getTheme } from "$lib/theme/themeUtils";

  let { children, bodyItems, class: className, ...restProps }: TableBodyProps = $props();

  const theme = getTheme("tableBody");

  function getCellValues(row: BodyRow): CellValue[] {
    if (Array.isArray(row)) {
      return row;
    } else {
      return Object.values(row);
    }
  }
</script>

<tbody {...restProps} class={clsx(theme, className)}>
  {#if bodyItems}
    {#each bodyItems as row}
      <TableBodyRow>
        {#each getCellValues(row) as cellValue}
          <TableBodyCell>{cellValue ?? ""}</TableBodyCell>
        {/each}
      </TableBodyRow>
    {/each}
  {:else if children}
    {@render children()}
  {/if}
</tbody>

<!--
@component
[Go to docs](https://flowbite-svelte.com/)
## Type
[TableBodyProps](https://github.com/themesberg/flowbite-svelte/blob/main/src/lib/types.ts#L1651)
## Props
@prop children
@prop bodyItems
@prop class: className
@prop ...restProps
-->
