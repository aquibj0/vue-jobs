<script setup>
import { defineProps } from 'vue';

defineProps({
    bg: {
        type: String,
        default: 'bg-gray-100'
    }
});

</script>
<template>

    <div :class="`${bg} p-6 rounded-lg shadow-lg`">
        <slot></slot>
    </div>

</template>