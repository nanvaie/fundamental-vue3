<template>
    <div :class="customClass">
        <slot />
    </div>
</template>

<script setup>

import { computed } from 'vue';

const props = defineProps({
    fullWidth: {
        type: Boolean,
        default: false,
    }
});

const BASE_CLASS = 'fd-bar__element';

const customClass = computed(() => props.fullWidth ? `${ BASE_CLASS } ${ BASE_CLASS }--full-width` : `${ BASE_CLASS }`);

</script>
