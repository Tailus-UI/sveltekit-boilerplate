<script lang="ts">
  import { createAccordion, melt } from '@melt-ui/svelte';
  import {accordion as accordionTheme} from '@tailus/themer-accordion'
  import { slide } from 'svelte/transition';
 
  const {
    elements: { content, item, trigger, root },
    helpers: { isSelected },
  } = createAccordion({
    defaultValue: 'item-1',
  });

  const items = [
    {
        id:"item-1",
        question: "What is Tailus Themer?",
        answer: "Tailus Themer is a versatile theming library designed to help you create modern and custom web User Interfaces with Tailwind CSS."
    },
    {
        id:"item-2",
        question: "What are the supported frameworks?",
        answer: "Tailus Themer is framework-agnostic and can be used with any front-end framework that supports Tailwind CSS, such as React, Vue, Angular, and others."
    },
    {
        id:"item-3",
        question: "Is it customizable?",
        answer: "Yes, Tailus Themer is highly customizable. It allows you to customize all aspects of your theme, including colors, typography, and more. You can also export your theme configuration to use in other projects."
    }
]
</script>
 
<div
  class="max-w-md mx-auto w-full"
  {...$root}
>
  {#each items as { id, question, answer }, i}
    <div
      {...$item(id)} use:item
      class={accordionTheme.item}
    >
      <h2>
        <button
          {...$trigger(id)} use:trigger
          class={accordionTheme.trigger.parent}
        >
          {question}
          <svg class={accordionTheme.trigger.icon + ($isSelected(id) && ' rotate-180')} xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
          </svg>
        </button>
      </h2>
      {#if $isSelected(id)}
        <div
          {...$content(id)} use:content
          transition:slide={{duration: 300}}
        >
          <div class={accordionTheme.content + " pb-6"}>
            {answer}
          </div>
        </div>
      {/if}
    </div>
  {/each}
</div>