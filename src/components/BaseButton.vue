<script setup>
    import { computed } from "vue"

    const props = defineProps({
        themeColor: {
            type: String,
            default: "primary",
            validator(value) {
                return ["default", "primary", "success", "danger"].includes(
                    value
                )
            },
        },
        layout: {
            type: String,
            default: "inline-block",
            validator(value) {
                return ["inline-block", "block"].includes(value)
            },
        },
    })

    const { classOfButton } = useClassOfButton(props)

    function useClassOfButton(props) {
        const display = computed(() => {
            let result = ""

            switch (props.layout) {
                case "inline-block":
                    result = "inline-block"
                    break
                case "block":
                    result = "w-full"
                    break
                default:
                    result = "inline-block"
                    break
            }

            return result
        })

        const backgroundColor = computed(() => {
            let result = ""

            switch (props.themeColor) {
                case "primary":
                    result = "bg-slate-700 text-white"
                    break
                case "success":
                    result = "bg-emerald-500"
                    break
                case "danger":
                    result = "bg-rose-600"
                    break
                default:
                    result = "bg-slate-100"
                    break
            }

            return result
        })

        const classOfButton = computed(() => {
            return [display.value, backgroundColor.value]
        })

        return {
            classOfButton,
        }
    }
</script>

<template>
    <button
        class="rounded-sm px-4 py-2 hover:opacity-90 text-sm"
        :class="classOfButton"
    >
        <slot>Text</slot>
    </button>
</template>

<style scoped></style>
