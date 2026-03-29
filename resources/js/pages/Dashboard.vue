<script setup lang="ts">
import { Head, usePage } from '@inertiajs/vue3';
import {
    Activity,
    ArrowUpRight,
    CheckCircle2,
    Clock,
    FileText,
    FolderKanban,
    MoreHorizontal,
    Plus,
    Star,
    TrendingUp,
    Users,
    Zap,
} from 'lucide-vue-next';
import { computed } from 'vue';
import { dashboard } from '@/routes';

defineOptions({
    layout: {
        breadcrumbs: [
            {
                title: 'Dashboard',
                href: dashboard(),
            },
        ],
    },
});

const page = usePage();
const user = computed(() => page.props.auth.user);
const firstName = computed(
    () => user.value.name?.split(' ')[0] || 'there',
);

const greeting = computed(() => {
    const hour = new Date().getHours();

    if (hour < 12) {
        return 'Good morning';
    }

    if (hour < 18) {
        return 'Good afternoon';
    }

    return 'Good evening';
});
</script>

<template>
    <Head title="Dashboard" />

    <div class="flex h-full flex-1 flex-col gap-6 p-4 md:p-6">
        <!-- Greeting -->
        <div class="flex flex-col gap-1 sm:flex-row sm:items-end sm:justify-between">
            <div>
                <h1
                    class="text-2xl font-semibold tracking-tight text-foreground"
                >
                    {{ greeting }}, {{ firstName }} 👋
                </h1>
                <p class="mt-1 text-sm text-muted-foreground">
                    Here's what's happening with your projects today.
                </p>
            </div>
            <button
                class="mt-3 inline-flex items-center gap-2 rounded-xl bg-primary px-4 py-2.5 text-sm font-medium text-primary-foreground shadow-sm transition-all hover:opacity-90 sm:mt-0"
            >
                <Plus class="h-4 w-4" />
                New Project
            </button>
        </div>

        <!-- Stats Grid -->
        <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4">
            <!-- Total Projects -->
            <div
                class="group relative overflow-hidden rounded-2xl border border-sidebar-border/50 bg-card p-5 transition-all duration-300 hover:shadow-md dark:border-sidebar-border"
            >
                <div class="flex items-center justify-between">
                    <div
                        class="flex h-10 w-10 items-center justify-center rounded-xl bg-blue-500/10 text-blue-600 dark:text-blue-400"
                    >
                        <FolderKanban class="h-5 w-5" />
                    </div>
                    <span
                        class="inline-flex items-center gap-1 rounded-full bg-emerald-500/10 px-2 py-0.5 text-xs font-medium text-emerald-600 dark:text-emerald-400"
                    >
                        <TrendingUp class="h-3 w-3" />
                        +12%
                    </span>
                </div>
                <div class="mt-4">
                    <p class="text-2xl font-bold text-foreground">24</p>
                    <p class="mt-0.5 text-xs text-muted-foreground">
                        Total Projects
                    </p>
                </div>
            </div>

            <!-- Active Tasks -->
            <div
                class="group relative overflow-hidden rounded-2xl border border-sidebar-border/50 bg-card p-5 transition-all duration-300 hover:shadow-md dark:border-sidebar-border"
            >
                <div class="flex items-center justify-between">
                    <div
                        class="flex h-10 w-10 items-center justify-center rounded-xl bg-amber-500/10 text-amber-600 dark:text-amber-400"
                    >
                        <Activity class="h-5 w-5" />
                    </div>
                    <span
                        class="inline-flex items-center gap-1 rounded-full bg-emerald-500/10 px-2 py-0.5 text-xs font-medium text-emerald-600 dark:text-emerald-400"
                    >
                        <TrendingUp class="h-3 w-3" />
                        +8%
                    </span>
                </div>
                <div class="mt-4">
                    <p class="text-2xl font-bold text-foreground">142</p>
                    <p class="mt-0.5 text-xs text-muted-foreground">
                        Active Tasks
                    </p>
                </div>
            </div>

            <!-- Team Members -->
            <div
                class="group relative overflow-hidden rounded-2xl border border-sidebar-border/50 bg-card p-5 transition-all duration-300 hover:shadow-md dark:border-sidebar-border"
            >
                <div class="flex items-center justify-between">
                    <div
                        class="flex h-10 w-10 items-center justify-center rounded-xl bg-violet-500/10 text-violet-600 dark:text-violet-400"
                    >
                        <Users class="h-5 w-5" />
                    </div>
                    <span
                        class="inline-flex items-center gap-1 rounded-full bg-emerald-500/10 px-2 py-0.5 text-xs font-medium text-emerald-600 dark:text-emerald-400"
                    >
                        <TrendingUp class="h-3 w-3" />
                        +3
                    </span>
                </div>
                <div class="mt-4">
                    <p class="text-2xl font-bold text-foreground">16</p>
                    <p class="mt-0.5 text-xs text-muted-foreground">
                        Team Members
                    </p>
                </div>
            </div>

            <!-- Completion Rate -->
            <div
                class="group relative overflow-hidden rounded-2xl border border-sidebar-border/50 bg-card p-5 transition-all duration-300 hover:shadow-md dark:border-sidebar-border"
            >
                <div class="flex items-center justify-between">
                    <div
                        class="flex h-10 w-10 items-center justify-center rounded-xl bg-emerald-500/10 text-emerald-600 dark:text-emerald-400"
                    >
                        <CheckCircle2 class="h-5 w-5" />
                    </div>
                    <span
                        class="inline-flex items-center gap-1 rounded-full bg-emerald-500/10 px-2 py-0.5 text-xs font-medium text-emerald-600 dark:text-emerald-400"
                    >
                        <TrendingUp class="h-3 w-3" />
                        +5%
                    </span>
                </div>
                <div class="mt-4">
                    <p class="text-2xl font-bold text-foreground">89%</p>
                    <p class="mt-0.5 text-xs text-muted-foreground">
                        Completion Rate
                    </p>
                </div>
            </div>
        </div>

        <!-- Main Content Grid -->
        <div class="grid flex-1 grid-cols-1 gap-4 lg:grid-cols-3">
            <!-- Recent Activity -->
            <div
                class="col-span-1 flex flex-col rounded-2xl border border-sidebar-border/50 bg-card lg:col-span-2 dark:border-sidebar-border"
            >
                <div
                    class="flex items-center justify-between border-b border-sidebar-border/50 px-5 py-4 dark:border-sidebar-border"
                >
                    <div>
                        <h2
                            class="text-sm font-semibold text-foreground"
                        >
                            Recent Activity
                        </h2>
                        <p class="mt-0.5 text-xs text-muted-foreground">
                            Latest updates across your projects
                        </p>
                    </div>
                    <button
                        class="rounded-lg p-1.5 text-muted-foreground transition-colors hover:bg-accent hover:text-foreground"
                    >
                        <MoreHorizontal class="h-4 w-4" />
                    </button>
                </div>
                <div class="flex-1 divide-y divide-sidebar-border/50 dark:divide-sidebar-border">
                    <!-- Activity Items -->
                    <div
                        class="flex items-start gap-4 px-5 py-4 transition-colors hover:bg-accent/30"
                    >
                        <div
                            class="mt-0.5 flex h-8 w-8 shrink-0 items-center justify-center rounded-lg bg-blue-500/10 text-blue-600 dark:text-blue-400"
                        >
                            <FileText class="h-4 w-4" />
                        </div>
                        <div class="min-w-0 flex-1">
                            <p class="text-sm text-foreground">
                                <span class="font-medium">Design System</span>
                                — Updated component library with new tokens
                            </p>
                            <p class="mt-1 text-xs text-muted-foreground">
                                2 minutes ago
                            </p>
                        </div>
                        <ArrowUpRight
                            class="mt-1 h-3.5 w-3.5 shrink-0 text-muted-foreground/50"
                        />
                    </div>

                    <div
                        class="flex items-start gap-4 px-5 py-4 transition-colors hover:bg-accent/30"
                    >
                        <div
                            class="mt-0.5 flex h-8 w-8 shrink-0 items-center justify-center rounded-lg bg-emerald-500/10 text-emerald-600 dark:text-emerald-400"
                        >
                            <CheckCircle2 class="h-4 w-4" />
                        </div>
                        <div class="min-w-0 flex-1">
                            <p class="text-sm text-foreground">
                                <span class="font-medium">API Gateway</span>
                                — Deployed v2.4.1 to production
                            </p>
                            <p class="mt-1 text-xs text-muted-foreground">
                                18 minutes ago
                            </p>
                        </div>
                        <ArrowUpRight
                            class="mt-1 h-3.5 w-3.5 shrink-0 text-muted-foreground/50"
                        />
                    </div>

                    <div
                        class="flex items-start gap-4 px-5 py-4 transition-colors hover:bg-accent/30"
                    >
                        <div
                            class="mt-0.5 flex h-8 w-8 shrink-0 items-center justify-center rounded-lg bg-violet-500/10 text-violet-600 dark:text-violet-400"
                        >
                            <Users class="h-4 w-4" />
                        </div>
                        <div class="min-w-0 flex-1">
                            <p class="text-sm text-foreground">
                                <span class="font-medium">3 new members</span>
                                joined the Frontend team
                            </p>
                            <p class="mt-1 text-xs text-muted-foreground">
                                1 hour ago
                            </p>
                        </div>
                        <ArrowUpRight
                            class="mt-1 h-3.5 w-3.5 shrink-0 text-muted-foreground/50"
                        />
                    </div>

                    <div
                        class="flex items-start gap-4 px-5 py-4 transition-colors hover:bg-accent/30"
                    >
                        <div
                            class="mt-0.5 flex h-8 w-8 shrink-0 items-center justify-center rounded-lg bg-amber-500/10 text-amber-600 dark:text-amber-400"
                        >
                            <Star class="h-4 w-4" />
                        </div>
                        <div class="min-w-0 flex-1">
                            <p class="text-sm text-foreground">
                                <span class="font-medium">Mobile App</span>
                                — Reached 10k+ downloads milestone
                            </p>
                            <p class="mt-1 text-xs text-muted-foreground">
                                3 hours ago
                            </p>
                        </div>
                        <ArrowUpRight
                            class="mt-1 h-3.5 w-3.5 shrink-0 text-muted-foreground/50"
                        />
                    </div>

                    <div
                        class="flex items-start gap-4 px-5 py-4 transition-colors hover:bg-accent/30"
                    >
                        <div
                            class="mt-0.5 flex h-8 w-8 shrink-0 items-center justify-center rounded-lg bg-rose-500/10 text-rose-600 dark:text-rose-400"
                        >
                            <Zap class="h-4 w-4" />
                        </div>
                        <div class="min-w-0 flex-1">
                            <p class="text-sm text-foreground">
                                <span class="font-medium">Performance</span>
                                — Lighthouse score improved to 98
                            </p>
                            <p class="mt-1 text-xs text-muted-foreground">
                                5 hours ago
                            </p>
                        </div>
                        <ArrowUpRight
                            class="mt-1 h-3.5 w-3.5 shrink-0 text-muted-foreground/50"
                        />
                    </div>
                </div>
            </div>

            <!-- Quick Actions -->
            <div
                class="col-span-1 flex flex-col rounded-2xl border border-sidebar-border/50 bg-card dark:border-sidebar-border"
            >
                <div
                    class="border-b border-sidebar-border/50 px-5 py-4 dark:border-sidebar-border"
                >
                    <h2 class="text-sm font-semibold text-foreground">
                        Quick Actions
                    </h2>
                    <p class="mt-0.5 text-xs text-muted-foreground">
                        Frequently used shortcuts
                    </p>
                </div>
                <div class="flex flex-1 flex-col gap-2 p-4">
                    <button
                        class="flex items-center gap-3 rounded-xl border border-sidebar-border/30 px-4 py-3.5 text-left transition-all duration-200 hover:border-sidebar-border hover:bg-accent/50 dark:border-sidebar-border/50 dark:hover:border-sidebar-border"
                    >
                        <div
                            class="flex h-9 w-9 items-center justify-center rounded-lg bg-blue-500/10 text-blue-600 dark:text-blue-400"
                        >
                            <Plus class="h-4 w-4" />
                        </div>
                        <div>
                            <p
                                class="text-sm font-medium text-foreground"
                            >
                                New Project
                            </p>
                            <p class="text-xs text-muted-foreground">
                                Start from scratch
                            </p>
                        </div>
                    </button>

                    <button
                        class="flex items-center gap-3 rounded-xl border border-sidebar-border/30 px-4 py-3.5 text-left transition-all duration-200 hover:border-sidebar-border hover:bg-accent/50 dark:border-sidebar-border/50 dark:hover:border-sidebar-border"
                    >
                        <div
                            class="flex h-9 w-9 items-center justify-center rounded-lg bg-amber-500/10 text-amber-600 dark:text-amber-400"
                        >
                            <FileText class="h-4 w-4" />
                        </div>
                        <div>
                            <p
                                class="text-sm font-medium text-foreground"
                            >
                                Create Task
                            </p>
                            <p class="text-xs text-muted-foreground">
                                Add a new task
                            </p>
                        </div>
                    </button>

                    <button
                        class="flex items-center gap-3 rounded-xl border border-sidebar-border/30 px-4 py-3.5 text-left transition-all duration-200 hover:border-sidebar-border hover:bg-accent/50 dark:border-sidebar-border/50 dark:hover:border-sidebar-border"
                    >
                        <div
                            class="flex h-9 w-9 items-center justify-center rounded-lg bg-violet-500/10 text-violet-600 dark:text-violet-400"
                        >
                            <Users class="h-4 w-4" />
                        </div>
                        <div>
                            <p
                                class="text-sm font-medium text-foreground"
                            >
                                Invite Team
                            </p>
                            <p class="text-xs text-muted-foreground">
                                Add collaborators
                            </p>
                        </div>
                    </button>

                    <button
                        class="flex items-center gap-3 rounded-xl border border-sidebar-border/30 px-4 py-3.5 text-left transition-all duration-200 hover:border-sidebar-border hover:bg-accent/50 dark:border-sidebar-border/50 dark:hover:border-sidebar-border"
                    >
                        <div
                            class="flex h-9 w-9 items-center justify-center rounded-lg bg-emerald-500/10 text-emerald-600 dark:text-emerald-400"
                        >
                            <Clock class="h-4 w-4" />
                        </div>
                        <div>
                            <p
                                class="text-sm font-medium text-foreground"
                            >
                                Track Time
                            </p>
                            <p class="text-xs text-muted-foreground">
                                Start a timer
                            </p>
                        </div>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
