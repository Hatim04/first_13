<script setup lang="ts">
import type { HTMLAttributes } from 'vue';

defineOptions({
    inheritAttrs: false,
});

type Props = {
    className?: HTMLAttributes['class'];
};

defineProps<Props>();
</script>

<template>
    <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 166 166"
        :class="className"
        v-bind="$attrs"
    >
        <defs>
            <linearGradient
                id="logo-grad"
                x1="0"
                y1="0"
                x2="166"
                y2="166"
                gradientUnits="userSpaceOnUse"
            >
                <stop offset="0%" stop-color="#f53003" />
                <stop offset="100%" stop-color="#f59e0b" />
            </linearGradient>
        </defs>
        <rect width="166" height="166" rx="40" fill="url(#logo-grad)" />
        <path
            d="M83 35L45 57v44l38 22 38-22V57L83 35zm0 12l28 16v32L83 111 55 95V63l28-16z"
            fill="white"
            fill-opacity="0.95"
        />
        <path
            d="M83 63v32l28-16V63L83 47v16z"
            fill="white"
            fill-opacity="0.5"
        />
    </svg>
</template>
