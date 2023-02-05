<template>
    <a
        :aria-disabled="props.disabled"
        :class="customClass"
        :download="props.download"
        :href="props.href"
        :referrerpolicy="props.referrerpolicy"
        :rel="props.rel"
        :target="props.target"
        :type="props.type"
    >
        <span class="fd-link__content"><slot /></span>
    </a>
</template>

<script setup>

import LinkDesign from '../assets/js/enums/LinkDesign';
import 'fundamental-styles/dist/link.css';

const props = defineProps({
    design: {
        type: String,
        default: LinkDesign.DEFAULT,
        validator(value) {
            return [
                LinkDesign.DEFAULT,
                LinkDesign.EMPHASIZED,
                LinkDesign.SUBTLE,
            ].includes(value);
        },
    },
    disabled: {
        type: Boolean,
        default: undefined,
    },
    download: String,
    href: String,
    inverted: {
        type: Boolean,
        default: undefined,
    },
    referrerpolicy: String,
    rel: String,
    target: String,
    type: String,
});

let customClass = 'fd-link';
if (props.design === LinkDesign.EMPHASIZED) {
    customClass += ' fd-link--emphasized';
} else if (props.design === LinkDesign.SUBTLE) {
    customClass += ' fd-link--subtle';
}

if (props.inverted) {
    customClass += ' fd-link--inverted';
}

</script>
