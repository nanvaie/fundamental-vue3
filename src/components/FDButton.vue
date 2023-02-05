<template>
    <button
        :class="customClass"
        :disabled="props.disabled"
    >
        <slot name="icon-start">
            <FDIcon v-if="iconStart" :name="iconStart"/>
        </slot>

        <slot></slot>

        <slot name="icon-end">
            <FDIcon v-if="iconStart" :name="iconEnd"/>
        </slot>

        <span class="fd-button__badge" v-if="isShowBadge">
            <slot name="badge"/>
        </span>
    </button>
</template>

<script setup>
    import { computed, useSlots } from "vue";
    import 'fundamental-styles/dist/button.css';
    import ButtonDesign from "../assets/js/enums/ButtonDesign.js";
    import FDIcon from './FDIcon.vue'

    const slots = useSlots();

    const props = defineProps({
        design: {
            type: String,
            default: ButtonDesign.DEFAULT,
            validator(value) {
                return [
                    ButtonDesign.GHOST,
                    ButtonDesign.DEFAULT,
                    ButtonDesign.NEGATIVE,
                    ButtonDesign.POSITIVE,
                    ButtonDesign.ATTENTION,
                    ButtonDesign.EMPHASIZED,
                    ButtonDesign.TRANSPARENT,
                ].includes(value);
            },
        },
        disabled: {
            type: Boolean,
            default: false,
        },
        iconEnd: String,
        iconStart: String,
    })

    const isShowBadge = computed(() => !!slots.badge)
    const customClass = computed(() => props.design !== ButtonDesign.DEFAULT ? `fd-button fd-button--${ props.design }` : 'fd-button')
</script>