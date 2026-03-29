<script setup lang="ts">
import { Link } from '@inertiajs/vue3';
import AppLogoIcon from '@/components/AppLogoIcon.vue';
import { home } from '@/routes';

defineProps<{
    title?: string;
    description?: string;
}>();
</script>

<template>
    <div
        class="relative flex min-h-svh flex-col items-center justify-center overflow-hidden bg-[#FAFAFA] p-6 md:p-10 dark:bg-[#09090B]"
    >
        <!-- Ambient background effects -->
        <div
            class="pointer-events-none absolute inset-0 overflow-hidden"
            aria-hidden="true"
        >
            <div
                class="absolute -top-[30%] left-1/2 h-[60vh] w-[60vh] -translate-x-1/2 rounded-full opacity-[0.06] blur-[100px] dark:opacity-[0.10]"
                style="
                    background: radial-gradient(
                        circle,
                        #f53003 0%,
                        transparent 70%
                    );
                "
            />
            <div
                class="absolute -bottom-[20%] -right-[10%] h-[40vh] w-[40vh] rounded-full opacity-[0.04] blur-[80px] dark:opacity-[0.06]"
                style="
                    background: radial-gradient(
                        circle,
                        #f59e0b 0%,
                        transparent 70%
                    );
                "
            />
        </div>

        <!-- Subtle grid -->
        <div
            class="pointer-events-none absolute inset-0 opacity-[0.025] dark:opacity-[0.035]"
            aria-hidden="true"
            style="
                background-image: linear-gradient(
                        rgba(0, 0, 0, 0.4) 1px,
                        transparent 1px
                    ),
                    linear-gradient(
                        90deg,
                        rgba(0, 0, 0, 0.4) 1px,
                        transparent 1px
                    );
                background-size: 60px 60px;
            "
        />

        <div class="relative z-10 w-full max-w-sm">
            <div class="flex flex-col gap-8">
                <!-- Logo + Title -->
                <div class="flex flex-col items-center gap-4">
                    <Link
                        :href="home()"
                        class="group flex flex-col items-center gap-3 font-medium transition-opacity hover:opacity-80"
                    >
                        <div
                            class="flex h-12 w-12 items-center justify-center rounded-2xl shadow-lg shadow-black/5 transition-transform duration-300 group-hover:scale-105 dark:shadow-white/5"
                        >
                            <AppLogoIcon class="size-12" />
                        </div>
                        <span class="sr-only">{{ title }}</span>
                    </Link>
                    <div class="space-y-1.5 text-center">
                        <h1
                            class="text-xl font-semibold tracking-tight text-[#1b1b18] dark:text-white"
                        >
                            {{ title }}
                        </h1>
                        <p
                            class="text-sm text-[#1b1b18]/50 dark:text-neutral-500"
                        >
                            {{ description }}
                        </p>
                    </div>
                </div>

                <!-- Auth Form Content -->
                <div
                    class="rounded-2xl border border-[#1b1b18]/[0.06] bg-white/80 p-6 shadow-sm backdrop-blur-sm sm:p-8 dark:border-white/[0.06] dark:bg-white/[0.03]"
                >
                    <slot />
                </div>
            </div>
        </div>
    </div>
</template>
