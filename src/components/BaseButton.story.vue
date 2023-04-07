<script setup>
    import { logEvent } from "histoire/client"
</script>

<template>
    <Story>
        <Variant title="primary">
            <BaseButton theme="primary" @click="logEvent('click', $event)">
                primary
            </BaseButton>
        </Variant>
        <Variant title="secondary">
            <BaseButton theme="secondary" @click="logEvent('click', $event)">
                secondary
            </BaseButton>
        </Variant>
        <Variant title="default">
            <BaseButton @click="logEvent('click', $event)">default</BaseButton>
        </Variant>
    </Story>
</template>

<style scoped></style>
