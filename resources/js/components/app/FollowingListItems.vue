<script setup>
import Input from '../ui/input/Input.vue';
import { ref } from "vue";
import FollowingItem from './FollowingItem.vue';

const searchKeyword = ref('')

</script>

<template>
    <Input :model-value="searchKeyword" placeholder="Search..." class="w-full mt-4" />
        <div class="mt-3 h-[200px] lg:flex-1 overflow-auto">
            <div v-if="false" class="text-gray-400 text-center p-3">
                You don't have any followers yet.
            </div>
            <div v-else>
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />
                <FollowingItem image="https://picsum.photos/100" title="Joana Doe" />
                <FollowingItem image="https://picsum.photos/100" title="Albert Einstein" />

            </div>
        </div>
</template>