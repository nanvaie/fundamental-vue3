<template>
    <span :class="customClass" aria-label="Avatar">
        <slot></slot>
        <FDIcon :class="avatarIcon"/>
</span>
</template>

<script setup>
    import { computed } from "vue";
    // Components
    import FDIcon from "./FDIcon.vue"

    // Styles
    import 'fundamental-styles/dist/avatar.css';

    // Enums
    import Size from "../assets/js/enums/Size.js";
    import Color from "../assets/js/enums/Color.js";

    const props = defineProps({
        size: {
            type: String,
            default: Size.EXTRA_SMALL,
            validator(value) {
                [
                    Size.SMALL,
                    Size.EXTRA_SMALL,
                    Size.MEDIUM,
                    Size.LARGE,
                    Size.EXTRA_LARGE,
                ].includes(value)
            }
        },
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
        icon: String,
        tile: Boolean,
        shell: Boolean,
        circle: Boolean,
        placeHolder: Boolean
    })

    const BASE_CLASS = 'fd-avatar';

    const avatarIcon = computed(() => `${ BASE_CLASS }__icon sap-icon--${ props.icon }`);


    const customClass = computed(() => `${ BASE_CLASS } ${ BASE_CLASS }--${ props.size } ${ circleClass.value } ${ shellClass.value } ${ tileClass.value } ${ placeHolderClass.value } ${ colorClass.value }`);
    const circleClass = computed(() => props.circle ? `${ BASE_CLASS }--circle` : '');
    const shellClass = computed(() => props.shell ? `${ BASE_CLASS }--shell` : '');
    const colorClass = computed(() => props.color ? `${ BASE_CLASS }--${ props.color }` : '');
    const tileClass = computed(() => props.tile ? `${ BASE_CLASS }--tile` : '');
    const placeHolderClass = computed(() => props.placeHolder ? `${ BASE_CLASS }--placeholder` : '');
</script>