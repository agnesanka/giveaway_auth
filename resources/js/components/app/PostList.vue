<script setup lang="ts">
import PostItem from './PostItem.vue';
import {
    Dialog,
    DialogContent,
    DialogDescription,
    DialogHeader,
    DialogTitle,
} from '@/components/ui/dialog';
import PostModal from './PostModal.vue';
import { ref } from "vue";

defineProps({
    posts: Array
})

const showEditModal = ref(false);
const editPost = ref({});

const post1 = {
    user: {
        id: 1,
        avatar: 'https://randomuser.me/api/portraits/lego/7.jpg',
        name: 'Bethoveen'
    },
    group: null,
    attachments: [
        {
            id: 1,
            name: 'test.png',
            url: 'https://picsum.photos/1000',
            mime: 'image/png'
        },
        {
            id: 2,
            name: 'test2.png',
            url: 'https://picsum.photos/1000',
            mime: 'image/png'
        },
        {
            id: 3,
            name: 'test3.docx',
            url: '#',
            mime: 'application/msword'
        }
    ],
    body: '<p>Lorem ipsum dolor sit amet aliquip ecommodo consequat.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>',
    created_at: '2025-01-23 12:32'
}
const post2 = {
    user: {
        id: 1,
        avatar: 'https://randomuser.me/api/portraits/lego/6.jpg',
        name: 'Chuck Norris'
    },
    group: {
        id: 1,
        name: 'Laravel Devs'
    },
    body: '<p>Lorem ipsum dolor sit amet aliquip ecommodo consequat.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>',
    created_at: '2025-01-23 12:32'
}

function openEditModal(post) {
    editPost.value = post;
    showEditModal.value = true;
}
</script>

<template>
    <div class="overflow-auto">
        <PostItem v-for="post of posts" :key="post.id" :post="post" @editClick="openEditModal" />
        <Dialog :open="showEditModal" @update:open="val => showEditModal = val">
            <!-- <teleport to="body"> -->
            <DialogContent>
                <DialogHeader class="space-y-3">
                    <DialogTitle class="py-3 px-4 text-base bg-gray-100">Update post</DialogTitle>
                    <DialogDescription class="hidden" />
                </DialogHeader>

                <PostModal :post="editPost" />

            </DialogContent>
            <!-- </teleport> -->
        </Dialog>
    </div>
</template>