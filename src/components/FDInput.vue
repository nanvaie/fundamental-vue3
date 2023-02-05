<template>
    <input
        :value="modelValue"
        @input="updateValue"
        :type="type"
        :readonly="readonly"
        :placeholder="placeholder"
        :class="customClass"
    />
</template>

<script setup>
    import { computed } from "vue";
    import InputType from "../assets/js/enums/InputType.js";
    import InputDesign from "../assets/js/enums/InputDesign.js";
    import 'fundamental-styles/dist/input.css';

    const emit = defineEmits(['update:modelValue']);
    const updateValue = (event) => {
        emit('update:modelValue', event.target.value);
    }

    const props = defineProps({
        modelValue: String,
        placeholder: String,
        type: {
            default: InputType.TEXT,
            type: String,
            validator(value) {
                return [
                    InputType.TEXT,
                    InputType.FAX,
                    InputType.TEL,
                    InputType.URL,
                    InputType.FILE,
                    InputType.BUTTON,
                    InputType.CHECKBOX,
                    InputType.DATETIME_LOCAL,
                    InputType.EMAIL,
                    InputType.HIDDEN,
                    InputType.NUMBER,
                    InputType.PASSWORD,
                    InputType.SUBMIT,
                    InputType.RANGE,
                    InputType.RADIO,
                    InputType.SEARCH,
                    InputType.WEEK,
                    InputType.RESET,
                    InputType.TIME,
                    InputType.MONTH,
                ].includes(value);
            },
        },
        design: {
            default: InputDesign.DEFAULT,
            type: String,
            validator(value) {
                return [
                    InputDesign.ERROR,
                    InputDesign.DEFAULT,
                    InputDesign.SUCCESS,
                    InputDesign.WARNING,
                    InputDesign.INFORMATION,
                ].includes(value)
            }
        },
        readonly: Boolean,
    });

    const customClass = computed(() => props.design !== InputDesign.DEFAULT ? `fd-input is-${ props.design }` : 'fd-input');

</script>