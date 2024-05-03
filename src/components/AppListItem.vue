<script setup>
import AppListItemSquare from './AppListItemSquare.vue';

const props = defineProps({
    item: {
        type: Array,
        required: true
    },
    index: {
        type: Number,
        required: true
    }
})
</script>

<template>
    <ul class="appListItem" :id="props.index">
        <AppListItemSquare v-for="square of item" :number="square"/>
    </ul>
</template>

<style scoped>
.appListItem {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin: 40px 20px;
}
</style>