<script setup lang="ts">
import { cn } from '@/lib/utils';
import { useVModel } from '@vueuse/core';
import type { HTMLAttributes } from 'vue';
import { onMounted, ref } from "vue";

const props = defineProps<{
    defaultValue?: string | number;
    modelValue?: string | number;
    class?: HTMLAttributes['class'];
    placeholder?: string;
    autoResize: {
        type: Boolean,
        default: true,
    };
}>();

const input = ref(null);

const emits = defineEmits<{
    (e: 'update:modelValue', payload: string | number): void;
}>();

const modelValue = useVModel(props, 'modelValue', emits, {
    passive: true,
    defaultValue: props.defaultValue,
});

function onInputChange($event) {
    emits('update:modelValue', $event.target.value)
    adjustHeight()    
}

function adjustHeight() {
    if (props.autoResize) {
        input.value.style.height = 'auto';
        input.value.style.height = input.value.scrollHeight + 'px';
    }
}

onMounted( () => {
    adjustHeight()
})

</script>

<template>
    <textarea v-model="modelValue" :class="cn(
        'flex h-10 w-full rounded-md border border-input bg-background px-3 py-2 text-base ring-offset-background file:border-0 file:bg-transparent file:text-sm file:font-medium file:text-foreground placeholder:text-muted-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 md:text-sm',
        props.class,
    )" 
    :placeholder="placeholder" @input="onInputChange" ref="input"></textarea>
</template>
