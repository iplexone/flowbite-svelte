<script lang="ts">
  import { setContext } from "svelte";
  import { table as tableCls, TableHead, TableBody, type TableTheme } from ".";
  import clsx from "clsx";
  import { type TableProps, type TableCtxType } from "$lib";
  import { getTheme } from "$lib/theme/themeUtils";

  let { children, footerSlot, captionSlot, items, divClass = "relative overflow-x-auto", striped, hoverable, border = true, shadow, color = "default", class: className, ...restProps }: TableProps = $props();

  const theme = getTheme("table");

  const { base, table } = $derived(tableCls({ color, shadow }));

  let tableCtx: TableCtxType = {
    get striped() {
      return striped;
    },
    get hoverable() {
      return hoverable;
    },
    get border() {
      return border;
    },
    get color() {
      return color;
    }
  };

  setContext("tableCtx", tableCtx);
  let headItems = $derived(items && items.length > 0 ? Object.keys(items[0]).map((key) => ({ text: key.charAt(0).toUpperCase() + key.slice(1) })) : []);

  let bodyItems = $derived(items && items.length > 0 ? items.map((item) => Object.values(item)) : []);
</script>

<div class={base({ class: clsx((theme as TableTheme)?.base, divClass) })}>
  <table {...restProps} class={table({ class: clsx((theme as TableTheme)?.table, className) })}>
    {#if captionSlot}
      {@render captionSlot()}
    {/if}
    {#if items && items.length > 0}
      <TableHead {headItems} />
      <TableBody {bodyItems} />
    {:else if children}
      {@render children()}
    {/if}
    {#if footerSlot}
      {@render footerSlot()}
    {/if}
  </table>
</div>

<!--
@component
[Go to docs](https://flowbite-svelte.com/)
## Type
[TableProps](https://github.com/themesberg/flowbite-svelte/blob/main/src/lib/types.ts#L1619)
## Props
@prop children
@prop footerSlot
@prop captionSlot
@prop items
@prop divClass = "relative overflow-x-auto"
@prop striped
@prop hoverable
@prop border = true
@prop shadow
@prop color = "default"
@prop class: className
@prop ...restProps
-->
