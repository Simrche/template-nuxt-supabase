<template>
    <div class="flex flex-col">
        <label v-if="label" class="px-4">{{ label }}<span v-if="required">*</span></label>
        <input
            :type="type"
            :placeholder="placeholder"
            class="bg-white rounded-2xl h-10 px-4"
            @input="$emit('input', $event.target?.value)"
            :value="value"
            :min="min"
            :max="max"
        />
    </div>
</template>

<script setup lang="ts">
const props = withDefaults(
    defineProps<{
        placeholder?: string;
        label?: string;
        type?: string;
        value?: any;
        min?: string;
        max?: string;
        required?: boolean;
    }>(),
    {
        placeholder: undefined,
        label: undefined,
        type: "text",
        value: undefined,
        min: undefined,
        max: undefined,
        required: false,
    }
);
</script>
