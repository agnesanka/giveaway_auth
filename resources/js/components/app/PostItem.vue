<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue'
import { PencilIcon, TrashIcon, EllipsisVerticalIcon } from '@heroicons/vue/20/solid'
import { Button } from '@/components/ui/button';
import PostUserHeader from './PostUserHeader.vue';
import { router } from '@inertiajs/vue3';

const props = defineProps({
    post: Object
})

const emit = defineEmits(['editClick'])

function isImage(attachment) {
    const mime = attachment.mime.split('/')
    return mime[0].toLowerCase() === 'image'
}

function openEditModal(){
    emit('editClick', props.post)
}

function deletePost(){
    if(window.confirm('Are you sure you want to delete this post?')) {
        router.delete(route('post.destroy', props.post), {
            preserveScroll: true
        })
    }
}
</script>

<template>
    <div class="bg-white border rounded p-4 mb-3">
        <div class="flex items-center justify-between mb-3">
            <PostUserHeader :post="post" />
            <Menu as="div" class="relative inline-block text-left">
                <div>
                    <MenuButton class="size-8 rounded-full hover:bg-black/5 trasition flex items-center justify-center">
                        <EllipsisVerticalIcon class="size-5" aria-hidden="true" />
                    </MenuButton>
                </div>
                <transition enter-active-class="transition duration-100 ease-out"
                    enter-from-class="transform scale-95 opacity-0" enter-to-class="transform scale-100 opacity-100"
                    leave-active-class="transition duration-75 ease-in"
                    leave-from-class="transform scale-100 opacity-100" leave-to-class="transform scale-95 opacity-0">
                    <MenuItems
                        class="absolute right-0 mt-2 w-32 origin-top-right divide-y divide-gray-100 rounded-md bg-white shadow-lg ring-1 ring-black/5 focus:outline-none">
                        <div class="px-1 py-1">
                            <MenuItem v-slot="{ active }">
                            <button @click="openEditModal" :class="[
                                active ? 'bg-indigo-500 text-white' : 'text-gray-900',
                                'group flex w-full items-center rounded-md px-2 py-2 text-sm',
                            ]">
                                <PencilIcon class="mr-2 h-5 w-5" aria-hidden="true" />
                                Edit
                            </button>
                            </MenuItem>
                            <MenuItem v-slot="{ active }">
                            <button @click="deletePost"
                            :class="[
                                active ? 'bg-indigo-500 text-white' : 'text-gray-900',
                                'group flex w-full items-center rounded-md px-2 py-2 text-sm',
                            ]">
                                <TrashIcon class="mr-2 h-5 w-5" aria-hidden="true" />
                                Delete
                            </button>
                            </MenuItem>
                        </div>
                    </MenuItems>
                </transition>
            </Menu>
        </div>
        <div class="mb-3">
            <Disclosure v-slot="{ open }">
                <div v-if="!open" v-html="post.body.substring(0, 200)" />
                <template v-if="post.body.length > 200">
                    <DisclosurePanel>
                        <div v-html="post.body" />
                    </DisclosurePanel>
                    <div class="flex justify-end">
                        <DisclosureButton class="text-blue-500 hover:underline">
                            {{ open ? 'Read less' : 'Read more' }}
                        </DisclosureButton>
                    </div>
                </template>
            </Disclosure>
        </div>
        <div class="grid grid-cols-2 lg:grid-cols-3 gap-3 mb-3">
            <template v-for="attachment of post.attachments">
                <div
                    class="group bg-blue-100 aspect-square flex flex-col items-center justify-center text-gray-500 relative">
                    <!-- Download button -->
                    <button
                        class="opacity-0 group-hover:opacity-100 transition-all size-8 flex items-center justify-center bg-gray-700 text-gray-100 rounded absolute right-2 top-2 cursor-pointer hover:bg-gray-800">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="size-5">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="M3 16.5v2.25A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75V16.5M16.5 12 12 16.5m0 0L7.5 12m4.5 4.5V3" />
                        </svg>
                    </button>
                    <!--/ Download button -->
                    <img v-if="isImage(attachment)" :src="attachment.url" class="objet-cover aspect-square" />

                    <template v-else>
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="size-12">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="M19.5 14.25v-2.625a3.375 3.375 0 0 0-3.375-3.375h-1.5A1.125 1.125 0 0 1 13.5 7.125v-1.5a3.375 3.375 0 0 0-3.375-3.375H8.25m2.25 0H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 0 0-9-9Z" />
                        </svg>

                        {{ attachment.name }}
                    </template>
                </div>
            </template>
        </div>
        <div class="flex gap-2">
            <Button
                class="text-gray-800 flex gap-1 flex-1 items-center justify-center bg-gray-100 hover:bg-gray-200 rounded-lg py-2 px-4">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M6.633 10.25c.806 0 1.533-.446 2.031-1.08a9.041 9.041 0 0 1 2.861-2.4c.723-.384 1.35-.956 1.653-1.715a4.498 4.498 0 0 0 .322-1.672V2.75a.75.75 0 0 1 .75-.75 2.25 2.25 0 0 1 2.25 2.25c0 1.152-.26 2.243-.723 3.218-.266.558.107 1.282.725 1.282m0 0h3.126c1.026 0 1.945.694 2.054 1.715.045.422.068.85.068 1.285a11.95 11.95 0 0 1-2.649 7.521c-.388.482-.987.729-1.605.729H13.48c-.483 0-.964-.078-1.423-.23l-3.114-1.04a4.501 4.501 0 0 0-1.423-.23H5.904m10.598-9.75H14.25M5.904 18.5c.083.205.173.405.27.602.197.4-.078.898-.523.898h-.908c-.889 0-1.713-.518-1.972-1.368a12 12 0 0 1-.521-3.507c0-1.553.295-3.036.831-4.398C3.387 9.953 4.167 9.5 5 9.5h1.053c.472 0 .745.556.5.96a8.958 8.958 0 0 0-1.302 4.665c0 1.194.232 2.333.654 3.375Z" />
                </svg>
                Like
            </Button>
            <Button
                class="text-gray-800 flex gap-1 flex-1 items-center justify-center bg-gray-100 hover:bg-gray-200 rounded-lg py-2 px-4">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M20.25 8.511c.884.284 1.5 1.128 1.5 2.097v4.286c0 1.136-.847 2.1-1.98 2.193-.34.027-.68.052-1.02.072v3.091l-3-3c-1.354 0-2.694-.055-4.02-.163a2.115 2.115 0 0 1-.825-.242m9.345-8.334a2.126 2.126 0 0 0-.476-.095 48.64 48.64 0 0 0-8.048 0c-1.131.094-1.976 1.057-1.976 2.192v4.286c0 .837.46 1.58 1.155 1.951m9.345-8.334V6.637c0-1.621-1.152-3.026-2.76-3.235A48.455 48.455 0 0 0 11.25 3c-2.115 0-4.198.137-6.24.402-1.608.209-2.76 1.614-2.76 3.235v6.226c0 1.621 1.152 3.026 2.76 3.235.577.075 1.157.14 1.74.194V21l4.155-4.155" />
                </svg>
                Comment
            </Button>
        </div>
    </div>
</template>