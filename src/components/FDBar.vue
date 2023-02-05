<template>
    <div :class="customClass">
        <div class="fd-bar__left">
            <slot name="start-content" />
        </div>

        <div class="fd-bar__middle">
            <slot />
        </div>

        <div class="fd-bar__right">
            <slot name="end-content" />
        </div>
    </div>
</template>

<script setup>

import 'fundamental-styles/dist/bar.css';
import BarDesign from '../assets/js/enums/BarDesign.js';
import { computed } from 'vue';

const props = defineProps({
    design: {
        type: String,
        default: BarDesign.HEADER,
        validator(value) {
            return [
                BarDesign.HEADER,
                BarDesign.HEADER_WITH_SUBHEADER,
                BarDesign.SUBHEADER,
                BarDesign.FOOTER,
                BarDesign.FLOATING_FOOTER,
            ].includes(value);
        },
    },
    responsive: {
        type: Boolean,
        default: false,
    }
});

const BASE_CLASS = 'fd-bar';

const customClass = computed(() => props.design !== BarDesign.HEADER ? `${ BASE_CLASS } ${ BASE_CLASS }--${ props.design }` : `${ BASE_CLASS }`);

</script>
