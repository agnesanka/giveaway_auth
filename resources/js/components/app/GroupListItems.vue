<script setup>
import GroupItem from './GroupItem.vue';
import Input from '../ui/input/Input.vue';
import { ref } from "vue";

const searchKeyword = ref('')
</script>

<template>
    <Input :model-value="searchKeyword" placeholder="Search..." class="w-full mt-4" />
    <div class="mt-3 h-[200px] lg:flex-1 overflow-auto">
        <div v-if="false" class="text-gray-400 text-center p-3">
            You are not a part of any group.
        </div>
        <div v-else>
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Laravel Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />
            <GroupItem image="https://picsum.photos/100" title="Vue Devs"
                description="Lorem ipsum dolor sit amet consectetur adipisicing elit." />

        </div>
    </div>
</template>