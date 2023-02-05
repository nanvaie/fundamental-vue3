<template>
    <span :class="customClass">
        <slot name="icon-start">
            <FDIcon v-if="iconStart" :class="icon_start"/>
        </slot>

        <span class="fd-info-label__text">
            <slot></slot>
        </span>

        <slot name="icon-end">
            <FDIcon v-if="iconStart" :class="icon_end"/>
        </slot>
    </span>
</template>

<script setup>
    import { computed } from "vue";
    import FDIcon from './FDIcon.vue'
    import 'fundamental-styles/dist/info-label.css';
    import Color from "../assets/js/enums/Color.js";

    const props = defineProps({
        color: {
            type: String,
            default: undefined,
            validator(value) {
                [
                    Color.ACCENT_COLOR_1,
                    Color.ACCENT_COLOR_2,
                    Color.ACCENT_COLOR_3,
                    Color.ACCENT_COLOR_4,
                    Color.ACCENT_COLOR_5,
                    Color.ACCENT_COLOR_6,
                    Color.ACCENT_COLOR_7,
                    Color.ACCENT_COLOR_8,
                    Color.ACCENT_COLOR_9,
                    Color.ACCENT_COLOR_10,
                ].includes(value)
            }
        },
        iconEnd: String,
        numeric: Boolean,
        iconStart: String,
    })

    const BASE_CLASS = 'fd-info-label'

    const customClass = computed(() => `${ BASE_CLASS } ${ colorClass } ${ contrastClass }`)
    const contrastClass = computed(() => props.numeric ? `${ BASE_CLASS }--numeric` : '').value;
    const colorClass = computed(() => props.color ? `${ BASE_CLASS }--${ props.color }` : '').value;
    const icon_end = computed(() => props.iconEnd ? `${ BASE_CLASS }__icon sap-icon--${ props.iconEnd }` : "")
    const icon_start = computed(() => props.iconStart ? `${ BASE_CLASS }__icon sap-icon--${ props.iconStart }` : "")
</script>