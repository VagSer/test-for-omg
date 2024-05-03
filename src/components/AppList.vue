<script setup>
import AppListItem from './AppListItem.vue';
import { onMounted, ref } from 'vue';

const props = defineProps({
    list: {
        type: Array,
        required: true,
    }
})
</script>

<template>
    <h3>List component</h3>
    <ul class="mainList">
        <AppListItem v-for="item of list" :item="item.list" :index="item.index"/>
    </ul>
</template>

<style scoped>
.mainList {
    border: 1px solid;
    width: 90%;
    margin: 4px auto;
}
</style>