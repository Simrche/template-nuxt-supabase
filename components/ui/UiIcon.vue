<template>
    <span @click="$emit('click')" v-if="icon" :class="`text-${color} mdi mdi-${icon} text-${size}`"></span>
</template>

<script setup lang="ts">
withDefaults(
    defineProps<{
        icon: string;
        color?: string;
        size?: string;
    }>(),
    {
        icon: undefined,
        color: "black",
        size: "md",
    }
);
</script>
