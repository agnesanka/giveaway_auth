<script setup lang="ts">
import { cn } from '@/lib/utils';
import type { HTMLAttributes } from 'vue';

const props = defineProps<{ class?: HTMLAttributes['class'] }>();
</script>

<template>
    <div :class="cn('flex flex-col-reverse sm:flex-row sm:justify-start sm:gap-x-2', props.class)">
        <slot />
    </div>
</template>
