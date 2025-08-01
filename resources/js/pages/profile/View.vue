<script setup>
import { XMarkIcon, CheckCircleIcon, CameraIcon } from '@heroicons/vue/24/solid'
import { Button } from '@/components/ui/button';
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue'
import { usePage, useForm } from '@inertiajs/vue3';
import AppHeaderLayout from '@/layouts/app/AppHeaderLayout.vue';
import TabItem from './partials/TabItem.vue';
import Edit from './Edit.vue';
import { computed, ref } from 'vue';

const showNotification = ref(true);
const coverImageSrc = ref('');
const avatarImageSrc = ref('');
const page = usePage();
const authUser = page.props.auth.user;
const isMyProfile = computed(() => authUser && authUser.id === props.user.id);

const imagesForm = useForm({
    avatar: null,
    cover: null,
})

const props = defineProps({
    errors: Object,
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
    success: {
        type: String,
    },
    // User passed from the ProfileController
    user: {
        type: Object,
    }
});

function onCoverChange(event) {
    imagesForm.cover = event.target.files[0];

    if (imagesForm.cover) {
        const reader = new FileReader;
        reader.onload = () => {
            coverImageSrc.value = reader.result;
        }
        reader.readAsDataURL(imagesForm.cover);
    }
}

function onAvatarChange(event) {
    imagesForm.avatar = event.target.files[0];
    if (imagesForm.avatar) {
        const reader = new FileReader;
        reader.onload = () => {
            avatarImageSrc.value = reader.result;
        }
        reader.readAsDataURL(imagesForm.avatar);
    }
}

function resetCoverImage() {
    imagesForm.cover = null;
    coverImageSrc.value = null;
}


function resetAvatarImage() {
    imagesForm.avatar = null;
    avatarImageSrc.value = null;
}

function submitCoverImage() {
    showNotification.value = true; 
    imagesForm.post(route('profile.updateImage'), {
        onSuccess: () => {
            resetCoverImage()
            setTimeout(() => {
                showNotification.value = false
            }, 3000)
        }
    });
}


function submitAvatarImage() {
    showNotification.value = true; 
    imagesForm.post(route('profile.updateImage'), {
        onSuccess: () => {
            resetAvatarImage()
            setTimeout(() => {
                showNotification.value = false
            }, 3000)
        }
    });
}

</script>

<template>
    <AppHeaderLayout>
        <div class="max-w-[768px] w-full mx-auto h-full overflow-auto">
            <!-- Notification message -->
            <div v-if="showNotification && success"
                class="my-2 py-2 px-3 text-sm font-medium text-white bg-emerald-500">
                {{ success }}
            </div>
            <!-- Error message -->
            <div v-if="errors.cover" class="my-2 py-2 px-3 text-sm font-medium text-white bg-red-400">
                {{ errors.cover }}
            </div>
            <div class="group relative bg-white">
                <img :src="coverImageSrc || user.cover_url || '/img/default_cover.jpg'"
                    class="w-full h-[300px] object-cover" />
                <div class="absolute top-2 right-2">
                    <Button v-if="!coverImageSrc"
                        class="bg-gray-50 hover:bg-gray-100 text-gray-800 py-1 px-2 text-xs flex items-center opacity-0 group-hover:opacity-100 transition-all">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="size-3 mr-2">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="M6.827 6.175A2.31 2.31 0 0 1 5.186 7.23c-.38.054-.757.112-1.134.175C2.999 7.58 2.25 8.507 2.25 9.574V18a2.25 2.25 0 0 0 2.25 2.25h15A2.25 2.25 0 0 0 21.75 18V9.574c0-1.067-.75-1.994-1.802-2.169a47.865 47.865 0 0 0-1.134-.175 2.31 2.31 0 0 1-1.64-1.055l-.822-1.316a2.192 2.192 0 0 0-1.736-1.039 48.774 48.774 0 0 0-5.232 0 2.192 2.192 0 0 0-1.736 1.039l-.821 1.316Z" />
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="M16.5 12.75a4.5 4.5 0 1 1-9 0 4.5 4.5 0 0 1 9 0ZM18.75 10.5h.008v.008h-.008V10.5Z" />
                        </svg>

                        Update cover image
                        <input type="file" class="absolute left-0 top-0 bottom-0 right-0 opacity-0 cursor-pointer z-20"
                            @change="onCoverChange" />
                    </Button>
                    <div v-else class="flex gap-2 bg-white p-2 opacity-0 group-hover:opacity-100 transition-all">
                        <Button @click="resetCoverImage"
                            class="bg-gray-50 hover:bg-gray-100 text-gray-800 py-1 px-3 text-xs flex items-center">
                            <XMarkIcon />
                            Cancel
                        </Button>
                        <Button @click="submitCoverImage"
                            class="bg-gray-800 hover:bg-gray-900 text-gray-100 py-1 px-3 text-xs flex items-center">
                            <CheckCircleIcon />
                            Submit
                        </Button>
                    </div>
                </div>
                <div class="flex">
                    <div class="flex items-center justify-center relative group/avatar h-[128px] w-[128px] ml-[48px] -mt-[64px] rounded-full">
                        <!-- User's avatar -->
                        <img :src="avatarImageSrc || user.avatar_url || '/img/default_avatar.jpg'" class="w-full h-full object-cover rounded-full" />
                        <Button v-if="!avatarImageSrc"
                            class="absolute left-0 top-0 right-0 bottom-0 h-full bg-black/50 hover:bg-black/50 text-gray-200 rounded-full opacity-0 group-hover/avatar:opacity-100 flex items-center justify-center transition-all">
                            <CameraIcon class="size-8" />
                            <input type="file"
                                class="absolute left-0 top-0 bottom-0 right-0 opacity-0 cursor-pointer z-20"
                                @change="onAvatarChange" />
                        </Button>
                        <div v-else class=" absolute top-1 right-0 flex flex-col gap-2 ">
                            <Button @click="resetAvatarImage"
                                class="size-7 flex items-center justify-center bg-red-500/80 color-white rounded-full">
                                <XMarkIcon class="size-5" />
                            </Button> 
                            <Button @click="submitAvatarImage"
                                class="size-7 flex items-center justify-center bg-emerald-500/80 color-white rounded-full">
                                <CheckCircleIcon class="size-5" />
                            </Button>
                        </div>

                    </div>
                    <div class="flex justify-between items-center flex-1 p-4">
                        <h2 class="font-bold text-lg">{{ user.name }}</h2>
                    </div>
                </div>
            </div>
            <div class="border-t">
                <TabGroup>
                    <TabList class="flex bg-white">
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
                        <Tab v-if="isMyProfile" v-slot="{ selected }" as="template">
                            <TabItem text="My profile" :selected="selected" />
                        </Tab>
                    </TabList>

                    <TabPanels class="mt-2">
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
                        <TabPanel v-if="isMyProfile" class="">
                            <Edit :must-verify-email="mustVerifyEmail" :status="status" />
                        </TabPanel>
                    </TabPanels>
                </TabGroup>
            </div>
        </div>
    </AppHeaderLayout>

</template>
