<script setup>
import { Button } from '@/components/ui/button';
import {
    DialogFooter,
    DialogClose
} from '@/components/ui/dialog';
import { watchEffect } from 'vue';
import InputTextarea from './InputTextarea.vue';
import PostUserHeader from './PostUserHeader.vue';
import { useForm } from '@inertiajs/vue3';


const props = defineProps({
    post: {
        type: Object,
        required: true
    },
    modelValue: Boolean
})

const form = useForm({
    id: null,
    body: ''
})

const autoResize = {
    value: true
}

watchEffect(() => {
    if (props.post && props.post.body !== undefined) {
        form.id = props.post.id
        form.body = props.post.body
    }
})

function submit() {
    form.put(route('post.update', props.post.id), {
        preserveScroll: true
    })
}

</script>

<template>

    <div class="grid gap-2 p-3">
        <PostUserHeader :post="post" :show-time="false" class="mb-3" />
        <InputTextarea v-model="form.body" class="mb-3 w-full h-20" :auto-resize />
    </div>

    <DialogFooter class="py-3 px-4">
        <DialogClose as-child>
            <Button type="submit"
                class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 w-full"
                @click="submit">Submit
            </Button>
        </DialogClose>
    </DialogFooter>
</template>