<template>
    <AccordionHeader
        unstyled
        :pt="theme"
        :ptOptions="{
            mergeProps: ptViewMerge
        }"
    >
        <template #toggleicon="{ active }">
            <ChevronDown v-if="active" />
            <ChevronUp v-else />
        </template>
        <slot></slot>
    </AccordionHeader>
</template>

<script setup>
import ChevronUp from '@primevue/icons/chevrondown';
import ChevronDown from '@primevue/icons/chevronup';
import AccordionHeader from 'primevue/accordionheader';
import { ref } from 'vue';
import { ptViewMerge } from '../utils';

const theme = ref({
    root: `cursor-pointer disabled:pointer-events-none disabled:opacity-60 flex items-center justify-between p-[1.125rem] font-semibold
        bg-surface-0 dark:bg-surface-900 
        text-surface-500 dark:text-surface-400 
        hover:text-surface-700 dark:hover:text-surface-0 
        p-active:text-surface-700 dark:p-active:text-surface-0
        transition-colors duration-200
        focus-visible:outline focus-visible:outline-1 focus-visible:outline-offset-[-1px] focus-visible:outline-primary`,
    toggleicon: ``
});
</script>
