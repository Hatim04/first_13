<script setup lang="ts">
import { Form, Head } from '@inertiajs/vue3';
import { Mail } from 'lucide-vue-next';
import TextLink from '@/components/TextLink.vue';
import { Button } from '@/components/ui/button';
import { Spinner } from '@/components/ui/spinner';
import { logout } from '@/routes';
import { send } from '@/routes/verification';

defineOptions({
    layout: {
        title: 'Verify your email',
        description:
            "We've sent a verification link to your email. Click it to activate your account.",
    },
});

defineProps<{
    status?: string;
}>();
</script>

<template>
    <Head title="Email verification" />

    <div
        v-if="status === 'verification-link-sent'"
        class="mb-4 rounded-lg bg-green-50 p-3 text-center text-sm font-medium text-green-700 dark:bg-green-900/20 dark:text-green-400"
    >
        A new verification link has been sent to your email address.
    </div>

    <Form
        v-bind="send.form()"
        class="space-y-5 text-center"
        v-slot="{ processing }"
    >
        <div
            class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-blue-50 dark:bg-blue-900/20"
        >
            <Mail class="h-6 w-6 text-blue-600 dark:text-blue-400" />
        </div>

        <p class="text-sm text-muted-foreground">
            Didn't receive the email? Check your spam folder or request a
            new one.
        </p>

        <Button
            :disabled="processing"
            variant="secondary"
            class="rounded-xl"
        >
            <Spinner v-if="processing" />
            Resend verification email
        </Button>

        <TextLink
            :href="logout()"
            as="button"
            class="mx-auto block text-sm"
        >
            Sign out
        </TextLink>
    </Form>
</template>
