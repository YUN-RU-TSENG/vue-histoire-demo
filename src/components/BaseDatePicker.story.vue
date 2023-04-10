<script setup>
    import { ref } from "vue"

    const state = ref({
        date: undefined,
        label: "日期",
    })
</script>

<template>
    <Story title="Base/BaseDatePicker">
        <Variant>
            <BaseDatePicker
                v-bind="state"
                placeholder="請輸入日期"
                @update:date="(data) => (state.date = data)"
            ></BaseDatePicker>
        </Variant>
    </Story>
</template>

<style scoped></style>
