<script setup>
    import { computed } from "vue"

    const props = defineProps({
        theme: {
            type: String,
            default: "default",
        },
    })

    const styleClass = computed(() => {
        let style = null
        switch (props.theme) {
            case "primary":
                style = ["bg-slate-500", "text-slate-100"]
                break
            case "secondary":
                style = ["bg-slate-300", "text-slate-800"]
                break
            case "default":
                style = ["bg-white", "text-slate-800"]
        }
        return style
    })
</script>

<template>
    <button :class="['px-2', 'py-1', 'border-2', ...styleClass]">
        <slot>text</slot>
    </button>
</template>

<style scoped></style>
