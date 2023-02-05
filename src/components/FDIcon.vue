<template>
    <i :class="customClass"></i>
</template>

<script setup>
    import { computed } from "vue";

    const props = defineProps({
        name: String
    })

    const customClass = computed(() => props.name ? `sap-icon--${ props.name }` : "")

</script>
