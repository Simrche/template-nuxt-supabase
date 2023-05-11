<template>
    <h1 :class="`font-bold text-${size}`">
        <slot />
    </h1>
</template>

<script setup lang="ts">
withDefaults(
    defineProps<{
        size?: string;
    }>(),
    {
        size: "xl",
    }
);
</script>
