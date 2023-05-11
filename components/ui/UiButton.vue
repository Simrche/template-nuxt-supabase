<template>
    <button
        class="bg-red-500 rounded-2xl h-12 text-white w-full"
        @click="
            redirect();
            $emit('click');
        "
    >
        <slot />
    </button>
</template>

<script setup lang="ts">
import { useRouter } from "@nuxtjs/composition-api";

const props = defineProps<{
    to?: string;
}>();

const router = useRouter();

function redirect() {
    if (!props.to) return;

    router.push(props.to);
}
</script>
