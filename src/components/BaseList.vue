<script setup>
    defineProps({
        items: {
            type: Array,
            required: true,
        },
    })
</script>

<template>
    <ul class="p-1 bg-slate-500 mb-2">
        <li
            v-for="item in items"
            :key="item"
            class="p-1 bg-slate-100 mb-1 last-of-type:mb-0"
        >
            {{ item }}
        </li>
    </ul>
</template>

<style scoped></style>
