<template>
    <div :class="customClass" aria-hidden="false" aria-label="Loading">
        <div :class="circleClass"></div>
        <div :class="circleClass"></div>
        <div :class="circleClass"></div>
    </div>
    <div class="fd-busy-indicator-extended__label" v-if="label">{{ label }}</div>
</template>

<script setup>
    import 'fundamental-styles/dist/busy-indicator.css';
    import { computed } from "vue";
    import Size from "../assets/js/enums/Size.js";

    const props = defineProps({
        size: {
            type: String,
            default: undefined,
            validator(value) {
                [
                    Size.MEDIUM,
                    Size.LARGE
                ].includes(value)
            }
        },
        contrast: Boolean,
        label: String
    })

    const BASE_CLASS = 'fd-busy-indicator'
    const circleClass = `${ BASE_CLASS }__circle`
    const customClass = computed(() => `${ BASE_CLASS } ${ sizeClass } ${ contrastClass }`);
    const sizeClass = computed(() => props.size ? `${ BASE_CLASS }--${ props.size }` : '').value;
    const contrastClass = computed(() => props.contrast ? `${ BASE_CLASS }--contrast` : '').value;
</script>