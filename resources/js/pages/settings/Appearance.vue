<script setup lang="ts">
import { Head } from '@inertiajs/vue3';
import { Monitor, Moon, Sun } from 'lucide-vue-next';
import AppearanceTabs from '@/components/AppearanceTabs.vue';
import Heading from '@/components/Heading.vue';
import { useAppearance } from '@/composables/useAppearance';
import { edit } from '@/routes/appearance';

defineOptions({
    layout: {
        breadcrumbs: [
            {
                title: 'Appearance settings',
                href: edit(),
            },
        ],
    },
});

const { appearance, updateAppearance } = useAppearance();

const themes = [
    {
        value: 'light' as const,
        label: 'Light',
        description: 'Clean and bright interface',
        icon: Sun,
        preview: 'bg-white border-neutral-200',
        previewAccent: 'bg-neutral-100',
        previewText: 'bg-neutral-300',
    },
    {
        value: 'dark' as const,
        label: 'Dark',
        description: 'Easy on the eyes',
        icon: Moon,
        preview: 'bg-neutral-900 border-neutral-700',
        previewAccent: 'bg-neutral-800',
        previewText: 'bg-neutral-600',
    },
    {
        value: 'system' as const,
        label: 'System',
        description: 'Match your device settings',
        icon: Monitor,
        preview:
            'bg-gradient-to-br from-white to-neutral-900 border-neutral-400',
        previewAccent: 'bg-neutral-400',
        previewText: 'bg-neutral-500',
    },
];
</script>

<template>
    <Head title="Appearance settings" />

    <h1 class="sr-only">Appearance settings</h1>

    <div class="space-y-8">
        <div
            class="rounded-2xl border border-sidebar-border/50 bg-card dark:border-sidebar-border"
        >
            <div
                class="border-b border-sidebar-border/50 px-6 py-5 dark:border-sidebar-border"
            >
                <Heading
                    variant="small"
                    title="Theme"
                    description="Choose how the application looks to you"
                />
            </div>
            <div class="px-6 py-6">
                <div class="grid grid-cols-1 gap-4 sm:grid-cols-3">
                    <button
                        v-for="theme in themes"
                        :key="theme.value"
                        @click="updateAppearance(theme.value)"
                        :class="[
                            'group flex flex-col overflow-hidden rounded-xl border-2 transition-all duration-200',
                            appearance === theme.value
                                ? 'border-primary shadow-md'
                                : 'border-sidebar-border/50 hover:border-sidebar-border dark:border-sidebar-border dark:hover:border-neutral-600',
                        ]"
                    >
                        <!-- Preview -->
                        <div
                            :class="[
                                'flex h-24 flex-col gap-2 border-b p-3',
                                theme.preview,
                            ]"
                        >
                            <div
                                :class="[
                                    'h-2 w-12 rounded-full',
                                    theme.previewText,
                                ]"
                            />
                            <div
                                :class="[
                                    'h-6 w-full rounded-md',
                                    theme.previewAccent,
                                ]"
                            />
                            <div class="flex gap-2">
                                <div
                                    :class="[
                                        'h-3 w-16 rounded',
                                        theme.previewAccent,
                                    ]"
                                />
                                <div
                                    :class="[
                                        'h-3 w-10 rounded',
                                        theme.previewAccent,
                                    ]"
                                />
                            </div>
                        </div>
                        <!-- Label -->
                        <div class="flex items-center gap-3 px-4 py-3">
                            <component
                                :is="theme.icon"
                                class="h-4 w-4 text-muted-foreground"
                            />
                            <div class="text-left">
                                <p
                                    class="text-sm font-medium text-foreground"
                                >
                                    {{ theme.label }}
                                </p>
                                <p
                                    class="text-xs text-muted-foreground"
                                >
                                    {{ theme.description }}
                                </p>
                            </div>
                        </div>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
