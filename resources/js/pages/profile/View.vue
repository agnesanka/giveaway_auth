<script setup>
import { Button } from '@/components/ui/button';
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue'
import { usePage } from '@inertiajs/vue3';
import AppHeaderLayout from '@/layouts/app/AppHeaderLayout.vue';
import TabItem from './partials/TabItem.vue';
import Edit from './Edit.vue';
import { computed } from 'vue';

const page = usePage();
const authUser = page.props.auth.user;
const isMyProfile = computed(() => authUser && authUser.id === props.user.id)

const props = defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
    // User passed from the ProfileController
    user: {
        type: Object,
    }
});

</script>

<template>
    <AppHeaderLayout>
        <div class="w-[768px] mx-auto h-full overflow-auto">
            <div class="relative bg-white">
                <img src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/c547ba3d-624b-4a5d-892e-8458fd9952fa/d5zfrww-29cca157-7322-4da3-a20e-ee62518f8f7c.jpg?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcL2M1NDdiYTNkLTYyNGItNGE1ZC04OTJlLTg0NThmZDk5NTJmYVwvZDV6ZnJ3dy0yOWNjYTE1Ny03MzIyLTRkYTMtYTIwZS1lZTYyNTE4ZjhmN2MuanBnIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.HXmOjvUsAqRSW6tI9C0n4ywXvKjP_e9jC-Psww8cGNQ"
                    class="w-full h-[300px] object-cover" />
                <div class="flex">
                    <img src="https://randomuser.me/api/portraits/lego/0.jpg"
                        class="ml-[48px] h-[128px] w-[128px] -mt-[64px] rounded-full" />
                    <div class="flex justify-between items-center flex-1 p-4">
                        <h2 class="font-bold text-lg">{{ user.name }}</h2>
                        <Button v-if="isMyProfile">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                                stroke="currentColor" class="size-4 mr-2">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L6.832 19.82a4.5 4.5 0 0 1-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 0 1 1.13-1.897L16.863 4.487Zm0 0L19.5 7.125" />
                            </svg>
                            Edit profile
                        </Button>
                    </div>
                </div>
            </div>
            <div class="border-t">
                <TabGroup>
                    <TabList class="flex bg-white">
                        <Tab v-if="isMyProfile" v-slot="{ selected }" as="template">
                            <TabItem text="About" :selected="selected" />
                        </Tab>
                        <Tab v-slot="{ selected }" as="template">
                            <TabItem text="Posts" :selected="selected" />
                        </Tab>
                        <Tab v-slot="{ selected }" as="template">
                            <TabItem text="Followers" :selected="selected" />
                        </Tab>
                        <Tab v-slot="{ selected }" as="template">
                            <TabItem text="Followings" :selected="selected" />
                        </Tab>
                        <Tab v-slot="{ selected }" as="template">
                            <TabItem text="Photos" :selected="selected" />
                        </Tab>
                    </TabList>

                    <TabPanels class="mt-2">
                        <TabPanel v-if="isMyProfile" class="">
                            <Edit :must-verify-email="mustVerifyEmail" :status="status" />
                        </TabPanel>
                        <TabPanel class="bg-white p-5">
                            Posts
                        </TabPanel>
                        <TabPanel class="bg-white p-5">
                            Followers
                        </TabPanel>
                        <TabPanel class="bg-white p-5">
                            Followings
                        </TabPanel>
                        <TabPanel class="bg-white p-5">
                            Photos
                        </TabPanel>
                    </TabPanels>
                </TabGroup>
            </div>
        </div>
    </AppHeaderLayout>

</template>
