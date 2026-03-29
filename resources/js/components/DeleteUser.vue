<script setup lang="ts">
import { Form } from '@inertiajs/vue3';
import { AlertTriangle } from 'lucide-vue-next';
import { useTemplateRef } from 'vue';
import ProfileController from '@/actions/App/Http/Controllers/Settings/ProfileController';
import Heading from '@/components/Heading.vue';
import InputError from '@/components/InputError.vue';
import PasswordInput from '@/components/PasswordInput.vue';
import { Button } from '@/components/ui/button';
import {
    Dialog,
    DialogClose,
    DialogContent,
    DialogDescription,
    DialogFooter,
    DialogHeader,
    DialogTitle,
    DialogTrigger,
} from '@/components/ui/dialog';
import { Label } from '@/components/ui/label';

const passwordInput = useTemplateRef('passwordInput');
</script>

<template>
    <div
        class="rounded-2xl border border-red-200/50 bg-card dark:border-red-900/30"
    >
        <div
            class="border-b border-red-200/50 px-6 py-5 dark:border-red-900/30"
        >
            <Heading
                variant="small"
                title="Danger zone"
                description="Permanently delete your account and all data"
            />
        </div>
        <div class="px-6 py-6">
            <div
                class="flex items-start gap-3 rounded-xl bg-red-50 p-4 dark:bg-red-900/10"
            >
                <AlertTriangle
                    class="mt-0.5 h-5 w-5 shrink-0 text-red-500 dark:text-red-400"
                />
                <div class="space-y-1">
                    <p
                        class="text-sm font-medium text-red-700 dark:text-red-300"
                    >
                        This action is irreversible
                    </p>
                    <p class="text-sm text-red-600/80 dark:text-red-400/80">
                        Once your account is deleted, all of its resources and
                        data will be permanently removed. Please be certain.
                    </p>
                </div>
            </div>

            <div class="mt-4">
                <Dialog>
                    <DialogTrigger as-child>
                        <Button
                            variant="destructive"
                            class="rounded-xl"
                            data-test="delete-user-button"
                            >Delete account</Button
                        >
                    </DialogTrigger>
                    <DialogContent>
                        <Form
                            v-bind="ProfileController.destroy.form()"
                            reset-on-success
                            @error="() => passwordInput?.focus()"
                            :options="{
                                preserveScroll: true,
                            }"
                            class="space-y-6"
                            v-slot="{
                                errors,
                                processing,
                                reset,
                                clearErrors,
                            }"
                        >
                            <DialogHeader class="space-y-3">
                                <DialogTitle
                                    >Are you sure you want to delete your
                                    account?</DialogTitle
                                >
                                <DialogDescription>
                                    Once your account is deleted, all of its
                                    resources and data will also be permanently
                                    deleted. Please enter your password to
                                    confirm you would like to permanently delete
                                    your account.
                                </DialogDescription>
                            </DialogHeader>

                            <div class="grid gap-2">
                                <Label for="password" class="sr-only"
                                    >Password</Label
                                >
                                <PasswordInput
                                    id="password"
                                    name="password"
                                    ref="passwordInput"
                                    placeholder="Enter your password"
                                />
                                <InputError :message="errors.password" />
                            </div>

                            <DialogFooter class="gap-2">
                                <DialogClose as-child>
                                    <Button
                                        variant="secondary"
                                        class="rounded-xl"
                                        @click="
                                            () => {
                                                clearErrors();
                                                reset();
                                            }
                                        "
                                    >
                                        Cancel
                                    </Button>
                                </DialogClose>

                                <Button
                                    type="submit"
                                    variant="destructive"
                                    class="rounded-xl"
                                    :disabled="processing"
                                    data-test="confirm-delete-user-button"
                                >
                                    Delete account
                                </Button>
                            </DialogFooter>
                        </Form>
                    </DialogContent>
                </Dialog>
            </div>
        </div>
    </div>
</template>
