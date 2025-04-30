<script setup lang="ts">
import PostItem from './PostItem.vue';

defineProps({
    posts: Array
})

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
</script>

<template>
    <div class="flex-1 overflow-auto">
        <PostItem v-for="post of posts" :key="post.id" :post="post"/>
    </div>
</template>