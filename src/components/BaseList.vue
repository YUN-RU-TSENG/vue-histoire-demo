<script setup>
    defineProps({
        items: {
            type: Array,
            required: true,
        },
    })
</script>

<template>
    <ul class="p-3 bg-slate-300 mb-2 rounded-sm">
        <li
            v-for="(item, index) of items"
            :key="index"
            class="p-1 bg-slate-100 mb-1 last-of-type:mb-0 rounded-sm"
        >
            {{ item }}
        </li>
    </ul>
</template>

<style scoped></style>
