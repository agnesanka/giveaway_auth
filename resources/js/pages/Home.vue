<script setup lang="ts">
import CreatePost from '@/components/app/CreatePost.vue';
import FollowingList from '@/components/app/FollowingList.vue';
import GroupList from '@/components/app/GroupList.vue';
import PostList from '@/components/app/PostList.vue';
import AppHeaderLayout from '@/layouts/app/AppHeaderLayout.vue';
import { Head } from '@inertiajs/vue3';

defineProps({
    posts: Object
});
</script>

<template>

    <Head title="Social Media Website">
        <link rel="preconnect" href="https://rsms.me/" />
        <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
    </Head>

    <AppHeaderLayout>
        <div class="grid lg:grid-cols-12 gap-3 p-4 h-full">
            <div class="lg:col-span-3 lg:order-1 h-full overflow-hidden">
                <GroupList />
            </div>
            <div class="lg:col-span-3 lg:order-3 h-full overflow-hidden">
                <FollowingList />
            </div>
            <div class="lg:col-span-6 lg:order-2 h-full overflow-hidden flex flex-col">
                <CreatePost />
                <PostList :posts="posts.data" class="flex-1" />
            </div>
        </div>
    </AppHeaderLayout>
</template>
