<script setup>
    import { ref } from "vue"
    import { logEvent } from "histoire/client"

    const state = ref({
        layout: "inline-block",
        themeColor: "default",
    })
</script>

<template>
    <Story>
        <Variant>
            <template #default>
                <BaseButton
                    v-bind="state"
                    @click="($event) => logEvent('click', $event)"
                    >button text</BaseButton
                >
            </template>
            <template #controls>
                <HstSelect
                    v-model="state.themeColor"
                    title="themeColor(主題色)"
                    :options="{
                        primary: 'primary',
                        default: 'default',
                        success: 'success',
                        danger: 'danger',
                    }"
                />
                <HstSelect
                    v-model="state.layout"
                    title="layout(display)"
                    :options="{
                        block: 'block',
                        'inline-block': 'inline-block',
                    }"
                />
            </template>
        </Variant>
    </Story>
</template>

<style scoped></style>
