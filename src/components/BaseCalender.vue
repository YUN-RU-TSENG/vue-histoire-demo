<script setup>
    import dayjs from "dayjs"
    import { ref, computed } from "vue"

    const props = defineProps({
        open: {
            type: Boolean,
            required: true,
        },
        date: { type: String, default: undefined },
    })

    defineEmits(["update:open"])

    const currentTime = ref(dayjs(props.date))

    const currentMonth = computed(() => {
        return currentTime.value.format("MMMM")
    })

    const currentDatesOfMonth = computed(() => {
        return currentTime.value.daysInMonth()
    })

    function nextMonth() {
        currentTime.value = currentTime.value.add(1, "month").format("MMMM")
    }

    function previousMonth() {
        currentTime.value = currentTime.value
            .subtract(1, "month")
            .format("MMMM")
    }
</script>
<template>
    <div>
        <BaseButton></BaseButton>
        <div v-show="open" class="bg-slate-100 rounded-sm p-2">
            <button @click="nextMonth">上</button>
            <button @click="previousMonth">下</button>
            <h3>{{ currentMonth }}</h3>
            <div class="flex flex-wrap">
                <div
                    v-for="day in currentDatesOfMonth"
                    :key="day"
                    class="flex-[0_1_14.5%]"
                >
                    {{ day }}
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped></style>
