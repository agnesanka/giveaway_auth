<script setup lang="ts">
import { Head, Link, useForm, usePage } from '@inertiajs/vue3';
import { ref } from 'vue';

import DeleteUser from '@/components/DeleteUser.vue';
import HeadingSmall from '@/components/HeadingSmall.vue';
import InputError from '@/components/InputError.vue';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { type BreadcrumbItem, type SharedData, type User } from '@/types';

interface Props {
    mustVerifyEmail: boolean;
    status?: string;
}

defineProps<Props>();

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Profile settings',
        href: '/settings/profile',
    },
];

const page = usePage<SharedData>();
const user = page.props.auth.user as User;

const form = useForm({
    name: user.name,
    username: user.username,
    email: user.email,
});

const submit = () => {
    form.patch(route('profile.update'), {
        preserveScroll: true,
    });
};

const passwordInput = ref<HTMLInputElement | null>(null);
const currentPasswordInput = ref<HTMLInputElement | null>(null);

const passForm = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

const updatePassword = () => {
    passForm.put(route('password.update'), {
        preserveScroll: true,
        onSuccess: () => passForm.reset(),
        onError: (errors: any) => {
            if (errors.password) {
                passForm.reset('password', 'password_confirmation');
                if (passwordInput.value instanceof HTMLInputElement) {
                    passwordInput.value.focus();
                }
            }

            if (errors.current_password) {
                passForm.reset('current_password');
                if (currentPasswordInput.value instanceof HTMLInputElement) {
                    currentPasswordInput.value.focus();
                }
            }
        },
    });
};
</script>

<template>
    <div class="flex flex-col space-y-6 mb-2 mt-2 p-6 bg-white rounded-sm">
        <HeadingSmall title="Profile information" description="Update your name and email address" />

        <form @submit.prevent="submit" class="space-y-6">
            <div class="grid gap-2">
                <Label for="name">Name</Label>
                <Input id="name" class="mt-1 block w-full" v-model="form.name" required autocomplete="name"
                    placeholder="Full name" />
                <InputError class="mt-2" :message="form.errors.name" />
            </div>

            <div class="grid gap-2">
                <Label for="username">Userame</Label>
                <Input id="username" class="mt-1 block w-full" v-model="form.username" required autocomplete="username"
                    placeholder="Username" />
                <InputError class="mt-2" :message="form.errors.username" />
            </div>

            <div class="grid gap-2">
                <Label for="email">Email address</Label>
                <Input id="email" type="email" class="mt-1 block w-full" v-model="form.email" required
                    autocomplete="username" placeholder="Email address" />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div v-if="mustVerifyEmail && !user.email_verified_at">
                <p class="-mt-4 text-sm text-muted-foreground">
                    Your email address is unverified.
                    <Link :href="route('verification.send')" method="post" as="button"
                        class="text-foreground underline decoration-neutral-300 underline-offset-4 transition-colors duration-300 ease-out hover:!decoration-current dark:decoration-neutral-500">
                    Click here to resend the verification email.
                    </Link>
                </p>

                <div v-if="status === 'verification-link-sent'" class="mt-2 text-sm font-medium text-green-600">
                    A new verification link has been sent to your email address.
                </div>
            </div>

            <div class="flex items-center gap-4">
                <Button :disabled="form.processing">Save</Button>

                <Transition enter-active-class="transition ease-in-out" enter-from-class="opacity-0"
                    leave-active-class="transition ease-in-out" leave-to-class="opacity-0">
                    <p v-show="form.recentlySuccessful" class="text-sm text-neutral-600">Saved.</p>
                </Transition>
            </div>
        </form>
    </div>
    <div class="flex flex-col space-y-6 mb-2 p-6 bg-white rounded-sm">
        <HeadingSmall title="Update password"
            description="Ensure your account is using a long, random password to stay secure" />

        <form @submit.prevent="updatePassword" class="space-y-6">
            <div class="grid gap-2">
                <Label for="current_password">Current password</Label>
                <Input id="current_password" ref="currentPasswordInput" v-model="passForm.current_password" type="password"
                    class="mt-1 block w-full" autocomplete="current-password" placeholder="Current password" />
                <InputError :message="passForm.errors.current_password" />
            </div>

            <div class="grid gap-2">
                <Label for="password">New password</Label>
                <Input id="password" ref="passwordInput" v-model="passForm.password" type="password"
                    class="mt-1 block w-full" autocomplete="new-password" placeholder="New password" />
                <InputError :message="passForm.errors.password" />
            </div>

            <div class="grid gap-2">
                <Label for="password_confirmation">Confirm password</Label>
                <Input id="password_confirmation" v-model="passForm.password_confirmation" type="password"
                    class="mt-1 block w-full" autocomplete="new-password" placeholder="Confirm password" />
                <InputError :message="passForm.errors.password_confirmation" />
            </div>

            <div class="flex items-center gap-4">
                <Button :disabled="passForm.processing">Save password</Button>

                <Transition enter-active-class="transition ease-in-out" enter-from-class="opacity-0"
                    leave-active-class="transition ease-in-out" leave-to-class="opacity-0">
                    <p v-show="passForm.recentlySuccessful" class="text-sm text-neutral-600">Saved.</p>
                </Transition>
            </div>
        </form>
    </div>
    <DeleteUser class="bg-white p-6 rounded-sm"/>
</template>
