<script lang="ts">
  import { setContext } from "svelte";
  import { progressStepper } from ".";
  import { type ProgressStepperProps } from "$lib";
  import clsx from "clsx";
  import { getTheme } from "$lib/theme/themeUtils";
  import type { ProgressStepperTheme } from ".";

  let { children, steps = [], classes, ...restrorps }: ProgressStepperProps = $props();

  const theme = getTheme("progressStepper");

  setContext("stepperType", "progress");
</script>

<ol class={progressStepper.stepper({ class: clsx((theme as ProgressStepperTheme)?.stepper, classes?.progressstepper) })} {...restrorps}>
  {#if children}
    {@render children()}
  {:else if steps}
    {#each steps as step, index}
      <li
        class={progressStepper.item({
          status: step.status,
          isLast: index === steps.length - 1,
          class: clsx((theme as ProgressStepperTheme)?.item, classes?.progressstepperitem)
        })}
      >
        <span class={progressStepper.circle({ status: step.status, class: clsx((theme as ProgressStepperTheme)?.circle, classes?.progresssteppercircle) })}>
          {#if step.status === "completed"}
            {#if step.icon}
              <step.icon class={clsx(step.iconClass) || "h-5 w-5 lg:h-6 lg:w-6"} />
            {:else}
              <svg class="h-3.5 w-3.5 text-blue-600 lg:h-4 lg:w-4 dark:text-blue-300" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 16 12">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5.917 5.724 10.5 15 1.5" />
              </svg>
            {/if}
          {:else if step.icon}
            <step.icon class={clsx(step.iconClass) || "h-5 w-5 lg:h-6 lg:w-6"} />
          {:else}
            <svg class="h-4 w-4 text-gray-500 lg:h-5 lg:w-5 dark:text-gray-100" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 16">
              <path d="M18 0H2a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2ZM6.5 3a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5ZM3.014 13.021l.157-.625A3.427 3.427 0 0 1 6.5 9.571a3.426 3.426 0 0 1 3.322 2.805l.159.622-6.967.023ZM16 12h-3a1 1 0 0 1 0-2h3a1 1 0 0 1 0 2Zm0-3h-3a1 1 0 1 1 0-2h3a1 1 0 1 1 0 2Zm0-3h-3a1 1 0 1 1 0-2h3a1 1 0 1 1 0 2Z" />
            </svg>
          {/if}
        </span>
      </li>
    {/each}
  {/if}
</ol>

<!--
@component
[Go to docs](https://flowbite-svelte.com/)
## Type
[ProgressStepperProps](https://github.com/themesberg/flowbite-svelte/blob/main/src/lib/types.ts#L1527)
## Props
@prop children
@prop steps = []
@prop classes
@prop ...restrorps
-->
