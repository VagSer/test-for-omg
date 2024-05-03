<script setup>
const props = defineProps({
    number: {
        type: Number,
        required: true,
    }
})
</script>

<template>
    <li>
        {{ number }}
    </li>
</template>

<style scoped>
li {
    border: 1px solid;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
    width: 3rem;
    padding: 8px;
    aspect-ratio: 1/1;
    transition: 500ms;
    cursor: pointer;
    border-radius: 8px;

    &::marker {
        content: '';
    }

    &:hover {
        scale: 0.8;
    }
}
</style>