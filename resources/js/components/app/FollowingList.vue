<script setup> 
import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue';
import FollowingListItems from './FollowingListItems.vue';

</script>

<template>
    <div class="p-3 bg-white rounded border h-full overflow-hidden">
        <div class="h-full flex-1 block lg:hidden">
            <Disclosure v-slot="{ open }">
                <DisclosureButton class="w-full">
                    <div class="flex justify-between items-center">
                        <h2 class="text-xl font-bold">My Followings</h2>
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="size-6 transition-all" :class="open && 'rotate-90 transform'">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5" />
                        </svg>
                    </div>

                </DisclosureButton>
                <DisclosurePanel>
                    <FollowingListItems />
                </DisclosurePanel>

            </Disclosure>
        </div>

        <div class="h-full hidden lg:flex flex-1 flex-col overflow-hidden">
            <h2 class="text-xl font-bold">My Followings</h2>
            <FollowingListItems />
        </div>
    </div>
</template>