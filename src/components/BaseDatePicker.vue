<script setup>
    import { computed, ref, watchEffect } from "vue"
    import dayjs from "dayjs"

    const props = defineProps({
        date: {
            required: true,
            type: String,
        },
        label: {
            type: String,
            default: "",
        },
    })

    const emits = defineEmits(["update:date"])

    const {
        current,
        currentOfCalenderDisplayYear,
        currentOfCalenderDisplayMonth,
        currentDateOfCalenderDisplay,
        previousMonth,
        goPreviousMonth,
        nextMonth,
        goNextMonth,
        updateCurrent,
        currentOfCalenderDisplayWeekDayEmpty,
    } = useCalenderTime(props)
    const { isOpen, toggle } = useToggle()

    function useToggle() {
        const isOpen = ref(false)

        function toggle() {
            isOpen.value = !isOpen.value
        }

        function open() {
            isOpen.value = true
        }

        function close() {
            isOpen.value = false
        }

        return {
            isOpen,
            toggle,
            open,
            close,
        }
    }

    function useCalenderTime(props) {
        // 當前選擇時間
        const current = computed(() => {
            if (props.date) return dayjs(props.date)
            return dayjs()
        })

        // 當前面板時間點
        const currentOfCalenderDisplay = ref(current.value)
        watchEffect(() => {
            currentOfCalenderDisplay.value = current.value
        })

        // 當前面板時間點年份
        const currentOfCalenderDisplayYear = computed(() => {
            return currentOfCalenderDisplay.value.format("YYYY")
        })

        // 當前面板時間點月份
        const currentOfCalenderDisplayMonth = computed(() => {
            return currentOfCalenderDisplay.value.format("MMMM")
        })

        // 當前面板時間點月份總日期
        const currentDateOfCalenderDisplay = computed(() => {
            return Number(currentOfCalenderDisplay.value.daysInMonth())
        })

        // 當前面板時間點月份日期星期排版空格（例如一號是星期五，一週起始為週日，生成五個空格）
        const currentOfCalenderDisplayWeekDayEmpty = computed(() => {
            return currentOfCalenderDisplay.value.startOf("month").day()
        })

        // 當前面板呈現上一個月
        const previousMonth = computed(() => {
            return currentOfCalenderDisplay.value
                .subtract(1, "month")
                .format("MMMM")
        })

        function goPreviousMonth() {
            currentOfCalenderDisplay.value =
                currentOfCalenderDisplay.value.subtract(1, "month")
        }

        // 當前面板呈現下一個月
        const nextMonth = computed(() => {
            return currentOfCalenderDisplay.value.add(1, "month").format("MMMM")
        })

        function goNextMonth() {
            currentOfCalenderDisplay.value = currentOfCalenderDisplay.value.add(
                1,
                "month"
            )
        }

        function updateCurrent({ year, month, date }) {
            const data = dayjs([year, month, date]).format("YYYY/MM/DD")
            console.log({ year, month, date })
            emits("update:date", data)
        }

        console.log(
            current.value,
            currentOfCalenderDisplay,
            currentOfCalenderDisplayYear,
            currentOfCalenderDisplayMonth,
            currentDateOfCalenderDisplay,
            currentOfCalenderDisplayWeekDayEmpty,
            previousMonth,
            nextMonth,
            goPreviousMonth,
            goNextMonth,
            updateCurrent
        )

        return {
            current,
            currentOfCalenderDisplay,
            currentOfCalenderDisplayYear,
            currentOfCalenderDisplayMonth,
            currentDateOfCalenderDisplay,
            currentOfCalenderDisplayWeekDayEmpty,
            previousMonth,
            nextMonth,
            goPreviousMonth,
            goNextMonth,
            updateCurrent,
        }
    }

    const selectedDateStyled = computed(() => ({ year, month, date }) => {
        console.log(current.value.format("YYYY/MM/DD"))
        console.log()
        if (
            current.value.format("YYYY/MM/DD") ===
            dayjs([year, month, date]).format("YYYY/MM/DD")
        )
            return "text-emerald-500"
    })
</script>

<template>
    <label for="" class="inline-block relative text-slate-700">
        <span v-if="!!label" class="block text-sm">{{ label }}</span>
        <input
            type="text"
            class="bg-transparent border border-slate-700 py-2 px-4 text-base outline-0 rounded-sm"
            v-bind="$attrs"
            :value="date"
            @click="toggle"
        />
        <section
            v-show="isOpen"
            class="rounded-sm absolute top-full left-0 bg-slate-100"
        >
            <div class="p-2 flex justify-between">
                <BaseButton theme-color="default" @click="goPreviousMonth">{{
                    previousMonth
                }}</BaseButton>
                <BaseButton theme-color="default" @click="goNextMonth">{{
                    nextMonth
                }}</BaseButton>
            </div>
            <div class="text-center mb-2">
                {{
                    currentOfCalenderDisplayYear +
                    ", " +
                    currentOfCalenderDisplayMonth
                }}
            </div>
            <div class="flex flex-wrap gap-y-1 py-1">
                <div
                    v-for="(item, index) in [
                        '日',
                        '一',
                        '二',
                        '三',
                        '四',
                        '五',
                        '六',
                    ]"
                    :key="index"
                    class="flex-initial w-[14.28%] text-center py-1 relative text-sm"
                >
                    {{ item }}
                </div>
                <div
                    v-for="(_, index) in currentOfCalenderDisplayWeekDayEmpty"
                    :key="index"
                    class="flex-initial w-[14.28%] text-center py-1 hover:cursor-pointer hover:text-emerald-500 relative text-sm"
                ></div>
                <div
                    v-for="item in currentDateOfCalenderDisplay"
                    :key="item"
                    class="flex-initial w-[14.28%] text-center py-1 hover:cursor-pointer hover:text-emerald-500 relative text-sm"
                    :class="
                        selectedDateStyled({
                            year: currentOfCalenderDisplayYear,
                            month: currentOfCalenderDisplayMonth,
                            date: item,
                        })
                    "
                    @click="
                        () =>
                            updateCurrent({
                                year: currentOfCalenderDisplayYear,
                                month: currentOfCalenderDisplayMonth,
                                date: item,
                            })
                    "
                >
                    {{ item }}
                </div>
            </div>
            <div class="p-2 flex flex-row-reverse">
                <BaseButton theme-color="primary" @click="toggle"
                    >關閉</BaseButton
                >
            </div>
        </section>
    </label>
</template>

<style scoped></style>
