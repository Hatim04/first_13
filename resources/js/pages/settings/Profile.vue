<script setup lang="ts">
import { Form, Head, Link, usePage } from '@inertiajs/vue3';
import { computed } from 'vue';
import ProfileController from '@/actions/App/Http/Controllers/Settings/ProfileController';
import DeleteUser from '@/components/DeleteUser.vue';
import Heading from '@/components/Heading.vue';
import InputError from '@/components/InputError.vue';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { edit } from '@/routes/profile';
import { send } from '@/routes/verification';

type Props = {
    mustVerifyEmail: boolean;
    status?: string;
};

defineProps<Props>();

defineOptions({
    layout: {
        breadcrumbs: [
            {
                title: 'Profile settings',
                href: edit(),
            },
        ],
    },
});

const page = usePage();
const user = computed(() => page.props.auth.user);
</script>

<template>
    <Head title="Profile settings" />

    <h1 class="sr-only">Profile settings</h1>

    <div class="space-y-8">
        <!-- Profile Information Card -->
        <div
            class="rounded-2xl border border-sidebar-border/50 bg-card dark:border-sidebar-border"
        >
            <div
                class="border-b border-sidebar-border/50 px-6 py-5 dark:border-sidebar-border"
            >
                <Heading
                    variant="small"
                    title="Profile information"
                    description="Update your name and email address"
                />
            </div>
            <div class="px-6 py-6">
                <Form
                    v-bind="ProfileController.update.form()"
                    class="space-y-5"
                    v-slot="{ errors, processing, recentlySuccessful }"
                >
                    <div class="grid gap-1.5">
                        <Label for="name">Name</Label>
                        <Input
                            id="name"
                            name="name"
                            :default-value="user.name"
                            required
                            autocomplete="name"
                            placeholder="Full name"
                        />
                        <InputError :message="errors.name" />
                    </div>

                    <div class="grid gap-1.5">
                        <Label for="email">Email address</Label>
                        <Input
                            id="email"
                            type="email"
                            name="email"
                            :default-value="user.email"
                            required
                            autocomplete="username"
                            placeholder="Email address"
                        />
                        <InputError :message="errors.email" />
                    </div>

                    <div
                        v-if="mustVerifyEmail && !user.email_verified_at"
                    >
                        <p class="-mt-2 text-sm text-muted-foreground">
                            Your email address is unverified.
                            <Link
                                :href="send()"
                                as="button"
                                class="text-foreground underline decoration-neutral-300 underline-offset-4 transition-colors duration-300 ease-out hover:decoration-current! dark:decoration-neutral-500"
                            >
                                Click here to resend the verification
                                email.
                            </Link>
                        </p>

                        <div
                            v-if="status === 'verification-link-sent'"
                            class="mt-2 rounded-lg bg-green-50 p-2.5 text-sm font-medium text-green-700 dark:bg-green-900/20 dark:text-green-400"
                        >
                            A new verification link has been sent to
                            your email address.
                        </div>
                    </div>

                    <div class="flex items-center gap-4 pt-2">
                        <Button
                            class="rounded-xl"
                            :disabled="processing"
                            data-test="update-profile-button"
                            >Save changes</Button
                        >

                        <Transition
                            enter-active-class="transition ease-in-out"
                            enter-from-class="opacity-0"
                            leave-active-class="transition ease-in-out"
                            leave-to-class="opacity-0"
                        >
                            <p
                                v-show="recentlySuccessful"
                                class="text-sm text-emerald-600 dark:text-emerald-400"
                            >
                                Saved successfully.
                            </p>
                        </Transition>
                    </div>
                </Form>
            </div>
        </div>

        <!-- Delete Account -->
        <DeleteUser />
    </div>
</template>
