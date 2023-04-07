<script setup>
    import { ref } from "vue"

    const one = ref({
        open: true,
    })

    const two = ref({
        open: false,
    })
</script>

<template>
    <Story>
        <Variant title="open calender">
            <BaseCalender v-bind="one"></BaseCalender>
        </Variant>
        <Variant title="close calender">
            <BaseCalender v-bind="two"></BaseCalender>
        </Variant>
        <!-- <Variant title="select date">
            <BaseCalender></BaseCalender>
        </Variant>
        <Variant title="disable date">
            <BaseCalender></BaseCalender>
        </Variant> -->
    </Story>
</template>

<style scoped></style>
