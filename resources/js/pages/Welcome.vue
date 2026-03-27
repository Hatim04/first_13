<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';
import {
    ArrowRight,
    BookOpen,
    Cloud,
    Code2,
    Layers,
    Sparkles,
    Zap,
} from 'lucide-vue-next';
import { onMounted, ref } from 'vue';
import AppearanceTabs from '@/components/AppearanceTabs.vue';
import { dashboard, login, register } from '@/routes';

withDefaults(
    defineProps<{
        canRegister: boolean;
    }>(),
    {
        canRegister: true,
    },
);

const mounted = ref(false);

onMounted(() => {
    mounted.value = true;
});
</script>

<template>

    <Head title="Welcome">
        <link rel="preconnect" href="https://fonts.bunny.net" />
        <link href="https://fonts.bunny.net/css?family=instrument-sans:400,500,600,700" rel="stylesheet" />
    </Head>

    <div
        class="relative flex min-h-screen flex-col overflow-hidden bg-[#FAFAFA] text-[#1b1b18] dark:bg-[#09090B] dark:text-[#FAFAFA]">
        <!-- Ambient background effects -->
        <div class="pointer-events-none absolute inset-0 overflow-hidden" aria-hidden="true">
            <div class="absolute -top-[40%] left-1/2 h-[80vh] w-[80vh] -translate-x-1/2 rounded-full opacity-[0.08] blur-[120px] dark:opacity-[0.12]"
                style="
                    background: radial-gradient(
                        circle,
                        #f53003 0%,
                        transparent 70%
                    );
                " />
            <div class="absolute -right-[10%] -bottom-[20%] h-[60vh] w-[60vh] rounded-full opacity-[0.06] blur-[100px] dark:opacity-[0.08]"
                style="
                    background: radial-gradient(
                        circle,
                        #f59e0b 0%,
                        transparent 70%
                    );
                " />
            <div class="absolute -bottom-[20%] -left-[10%] h-[50vh] w-[50vh] rounded-full opacity-[0.04] blur-[100px] dark:opacity-[0.06]"
                style="
                    background: radial-gradient(
                        circle,
                        #6366f1 0%,
                        transparent 70%
                    );
                " />
        </div>

        <!-- Subtle grid background -->
        <div class="pointer-events-none absolute inset-0 opacity-[0.03] dark:opacity-[0.04]" aria-hidden="true" style="
                background-image:
                    linear-gradient(rgba(0, 0, 0, 0.5) 1px, transparent 1px),
                    linear-gradient(
                        90deg,
                        rgba(0, 0, 0, 0.5) 1px,
                        transparent 1px
                    );
                background-size: 60px 60px;
            " />

        <!-- Navigation -->
        <header class="relative z-10 w-full">
            <div class="mx-auto flex h-16 max-w-6xl items-center justify-between px-6 lg:h-20 lg:px-8">
                <!-- Logo -->
                <div class="flex items-center gap-3">
                    <div class="flex h-9 w-9 items-center justify-center rounded-lg bg-[#1b1b18] dark:bg-white">
                        <svg class="h-5 w-5 text-white dark:text-[#09090B]" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5" fill="none"
                                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                        </svg>
                    </div>
                    <span class="text-lg font-semibold tracking-tight text-[#1b1b18] dark:text-white">Laravel</span>
                </div>

                <!-- Auth Links -->
                <nav class="flex items-center gap-2">
                    <Link v-if="$page.props.auth.user" :href="dashboard()"
                        class="inline-flex items-center gap-2 rounded-full bg-[#1b1b18] px-5 py-2 text-sm font-medium text-white transition-all duration-200 hover:bg-[#333] dark:bg-white dark:text-[#09090B] dark:hover:bg-neutral-200">
                        Dashboard
                        <ArrowRight class="h-3.5 w-3.5" />
                    </Link>
                    <template v-else>
                        <Link :href="login()"
                            class="rounded-full px-5 py-2 text-sm font-medium text-[#1b1b18]/80 transition-colors duration-200 hover:text-[#1b1b18] dark:text-neutral-400 dark:hover:text-white">
                            Log in
                        </Link>
                        <Link v-if="canRegister" :href="register()"
                            class="inline-flex items-center gap-2 rounded-full bg-[#1b1b18] px-5 py-2 text-sm font-medium text-white transition-all duration-200 hover:bg-[#333] dark:bg-white dark:text-[#09090B] dark:hover:bg-neutral-200">
                            Get Started
                            <ArrowRight class="h-3.5 w-3.5" />
                        </Link>
                    </template>
                </nav>
            </div>
        </header>

        <!-- Hero Section -->
        <main class="relative z-10 flex flex-1 flex-col">
            <div class="mx-auto flex w-full max-w-6xl flex-1 flex-col items-center justify-center px-6 lg:px-8">
                <div class="flex flex-col items-center text-center" :class="{
                    'translate-y-0 opacity-100': mounted,
                    'translate-y-4 opacity-0': !mounted,
                }" style="transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1)">
                    <!-- Badge -->
                    <div
                        class="mb-6 inline-flex items-center gap-2 rounded-full border border-[#1b1b18]/10 bg-white/60 px-4 py-1.5 text-xs font-medium text-[#1b1b18]/70 backdrop-blur-sm sm:mb-8 dark:border-white/10 dark:bg-white/5 dark:text-neutral-400">
                        <Sparkles class="h-3.5 w-3.5 text-[#f53003]" />
                        Built with Laravel 13 & Vue
                    </div>

                    <!-- Main heading -->
                    <h1
                        class="max-w-3xl px-2 text-3xl font-bold tracking-tight text-[#1b1b18] sm:text-5xl lg:text-7xl dark:text-white">
                        Build something
                        <span
                            class="bg-gradient-to-r from-[#f53003] via-[#f59e0b] to-[#f53003] bg-clip-text text-transparent"
                            style="background-size: 200% auto">amazing</span>
                    </h1>

                    <p
                        class="mt-4 max-w-xl px-4 text-sm leading-relaxed text-[#1b1b18]/60 sm:mt-6 sm:px-0 sm:text-lg lg:text-xl dark:text-neutral-400">
                        The full-stack framework for artisans. Elegant syntax,
                        powerful tools, and everything you need to build modern
                        web applications.
                    </p>

                    <!-- CTA Buttons -->
                    <div class="mt-8 flex flex-col items-center gap-3 sm:mt-10 sm:flex-row sm:gap-4">
                        <Link v-if="!$page.props.auth.user" :href="register()"
                            class="group inline-flex items-center gap-2 rounded-full bg-[#1b1b18] px-7 py-3 text-sm font-semibold text-white shadow-lg shadow-black/10 transition-all duration-300 hover:scale-[1.02] hover:shadow-xl hover:shadow-black/15 dark:bg-white dark:text-[#09090B] dark:shadow-white/5 dark:hover:shadow-white/10">
                            Start Building
                            <ArrowRight class="h-4 w-4 transition-transform duration-200 group-hover:translate-x-0.5" />
                        </Link>
                        <Link v-if="$page.props.auth.user" :href="dashboard()"
                            class="group inline-flex items-center gap-2 rounded-full bg-[#1b1b18] px-7 py-3 text-sm font-semibold text-white shadow-lg shadow-black/10 transition-all duration-300 hover:scale-[1.02] hover:shadow-xl hover:shadow-black/15 dark:bg-white dark:text-[#09090B] dark:shadow-white/5 dark:hover:shadow-white/10">
                            Go to Dashboard
                            <ArrowRight class="h-4 w-4 transition-transform duration-200 group-hover:translate-x-0.5" />
                        </Link>
                        <a href="https://laravel.com/docs" target="_blank"
                            class="inline-flex items-center gap-2 rounded-full border border-[#1b1b18]/15 bg-white/50 px-7 py-3 text-sm font-semibold text-[#1b1b18] backdrop-blur-sm transition-all duration-300 hover:border-[#1b1b18]/25 hover:bg-white dark:border-white/10 dark:bg-white/5 dark:text-neutral-300 dark:hover:border-white/20 dark:hover:bg-white/10">
                            <BookOpen class="h-4 w-4" />
                            Documentation
                        </a>
                    </div>
                </div>

                <!-- Feature Cards -->
                <div class="mt-16 grid w-full max-w-4xl grid-cols-1 gap-3 px-2 sm:mt-20 sm:grid-cols-2 sm:gap-4 sm:px-0 lg:mt-24 lg:grid-cols-4 lg:gap-3"
                    :class="{
                        'translate-y-0 opacity-100': mounted,
                        'translate-y-8 opacity-0': !mounted,
                    }" style="
                        transition: all 1s cubic-bezier(0.16, 1, 0.3, 1) 0.2s;
                    ">
                    <!-- Card 1 -->
                    <a href="https://laravel.com/docs" target="_blank"
                        class="group relative overflow-hidden rounded-2xl border border-[#1b1b18]/[0.06] bg-white/70 p-5 backdrop-blur-sm transition-all duration-300 hover:border-[#1b1b18]/15 hover:shadow-lg hover:shadow-black/[0.03] dark:border-white/[0.06] dark:bg-white/[0.03] dark:hover:border-white/10 dark:hover:shadow-none">
                        <div
                            class="mb-4 inline-flex h-10 w-10 items-center justify-center rounded-xl bg-[#FEF2F2] transition-transform duration-300 group-hover:scale-110 dark:bg-[#f53003]/10">
                            <BookOpen class="h-5 w-5 text-[#f53003]" />
                        </div>
                        <h3 class="mb-1.5 text-sm font-semibold text-[#1b1b18] dark:text-white">
                            Documentation
                        </h3>
                        <p class="text-xs leading-relaxed text-[#1b1b18]/50 dark:text-neutral-500">
                            Comprehensive guides and API references to help you
                            get started.
                        </p>
                        <ArrowRight
                            class="absolute top-5 right-4 h-4 w-4 text-[#1b1b18]/20 transition-all duration-200 group-hover:translate-x-0.5 group-hover:text-[#1b1b18]/40 dark:text-white/10 dark:group-hover:text-white/30" />
                    </a>

                    <!-- Card 2 -->
                    <a href="https://laracasts.com" target="_blank"
                        class="group relative overflow-hidden rounded-2xl border border-[#1b1b18]/[0.06] bg-white/70 p-5 backdrop-blur-sm transition-all duration-300 hover:border-[#1b1b18]/15 hover:shadow-lg hover:shadow-black/[0.03] dark:border-white/[0.06] dark:bg-white/[0.03] dark:hover:border-white/10 dark:hover:shadow-none">
                        <div
                            class="mb-4 inline-flex h-10 w-10 items-center justify-center rounded-xl bg-[#FFF7ED] transition-transform duration-300 group-hover:scale-110 dark:bg-[#f59e0b]/10">
                            <Layers class="h-5 w-5 text-[#f59e0b]" />
                        </div>
                        <h3 class="mb-1.5 text-sm font-semibold text-[#1b1b18] dark:text-white">
                            Laracasts
                        </h3>
                        <p class="text-xs leading-relaxed text-[#1b1b18]/50 dark:text-neutral-500">
                            Thousands of video tutorials on Laravel, Vue, and
                            modern PHP.
                        </p>
                        <ArrowRight
                            class="absolute top-5 right-4 h-4 w-4 text-[#1b1b18]/20 transition-all duration-200 group-hover:translate-x-0.5 group-hover:text-[#1b1b18]/40 dark:text-white/10 dark:group-hover:text-white/30" />
                    </a>

                    <!-- Card 3 -->
                    <a href="https://cloud.laravel.com" target="_blank"
                        class="group relative overflow-hidden rounded-2xl border border-[#1b1b18]/[0.06] bg-white/70 p-5 backdrop-blur-sm transition-all duration-300 hover:border-[#1b1b18]/15 hover:shadow-lg hover:shadow-black/[0.03] dark:border-white/[0.06] dark:bg-white/[0.03] dark:hover:border-white/10 dark:hover:shadow-none">
                        <div
                            class="mb-4 inline-flex h-10 w-10 items-center justify-center rounded-xl bg-[#EFF6FF] transition-transform duration-300 group-hover:scale-110 dark:bg-[#3b82f6]/10">
                            <Cloud class="h-5 w-5 text-[#3b82f6]" />
                        </div>
                        <h3 class="mb-1.5 text-sm font-semibold text-[#1b1b18] dark:text-white">
                            Laravel Cloud
                        </h3>
                        <p class="text-xs leading-relaxed text-[#1b1b18]/50 dark:text-neutral-500">
                            Deploy your application with zero-downtime to the
                            cloud.
                        </p>
                        <ArrowRight
                            class="absolute top-5 right-4 h-4 w-4 text-[#1b1b18]/20 transition-all duration-200 group-hover:translate-x-0.5 group-hover:text-[#1b1b18]/40 dark:text-white/10 dark:group-hover:text-white/30" />
                    </a>

                    <!-- Card 4 -->
                    <a href="https://github.com/laravel/framework" target="_blank"
                        class="group relative overflow-hidden rounded-2xl border border-[#1b1b18]/[0.06] bg-white/70 p-5 backdrop-blur-sm transition-all duration-300 hover:border-[#1b1b18]/15 hover:shadow-lg hover:shadow-black/[0.03] dark:border-white/[0.06] dark:bg-white/[0.03] dark:hover:border-white/10 dark:hover:shadow-none">
                        <div
                            class="mb-4 inline-flex h-10 w-10 items-center justify-center rounded-xl bg-[#F5F3FF] transition-transform duration-300 group-hover:scale-110 dark:bg-[#8b5cf6]/10">
                            <Code2 class="h-5 w-5 text-[#8b5cf6]" />
                        </div>
                        <h3 class="mb-1.5 text-sm font-semibold text-[#1b1b18] dark:text-white">
                            Open Source
                        </h3>
                        <p class="text-xs leading-relaxed text-[#1b1b18]/50 dark:text-neutral-500">
                            Community-driven development. Contribute on GitHub.
                        </p>
                        <ArrowRight
                            class="absolute top-5 right-4 h-4 w-4 text-[#1b1b18]/20 transition-all duration-200 group-hover:translate-x-0.5 group-hover:text-[#1b1b18]/40 dark:text-white/10 dark:group-hover:text-white/30" />
                    </a>
                </div>
            </div>

            <!-- Footer -->
            <footer
                class="relative z-10 mt-auto border-t border-[#1b1b18]/[0.04] py-6 sm:py-8 dark:border-white/[0.04]">
                <div class="mx-auto flex max-w-6xl flex-col items-center gap-6 px-6 sm:gap-8 lg:px-8">
                    <!-- Highlights -->
                    <div
                        class="flex flex-wrap items-center justify-center gap-x-6 gap-y-3 text-xs text-[#1b1b18]/40 sm:gap-x-10 dark:text-neutral-600">
                        <div class="flex items-center gap-2">
                            <Zap class="h-3.5 w-3.5" />
                            <span>Lightning fast</span>
                        </div>
                        <div class="hidden h-3 w-px bg-[#1b1b18]/10 sm:block dark:bg-white/10" />
                        <div class="flex items-center gap-2">
                            <Layers class="h-3.5 w-3.5" />
                            <span>Full-stack</span>
                        </div>
                        <div class="hidden h-3 w-px bg-[#1b1b18]/10 sm:block dark:bg-white/10" />
                        <div class="flex items-center gap-2">
                            <Code2 class="h-3.5 w-3.5" />
                            <span>Developer first</span>
                        </div>
                        <div class="hidden h-3 w-px bg-[#1b1b18]/10 sm:block dark:bg-white/10" />
                        <div class="flex items-center gap-2">
                            <Cloud class="h-3.5 w-3.5" />
                            <span>Cloud ready</span>
                        </div>
                    </div>

                    <!-- Theme Toggle -->
                    <AppearanceTabs />
                </div>
            </footer>
        </main>
    </div>
</template>
