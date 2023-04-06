<script setup>
    import { ref, computed } from "vue"

    const items = ref(["a", "b", "c", "d", "e", "f"])
    const pageSize = ref(3)
    const currentPage = ref(0)

    const itemsOfCurrentPage = computed(() => {
        const begin = currentPage.value * pageSize.value
        return items.value.slice(begin, begin + 3)
    })

    const nextStep = () => {
        const totalPage = Math.ceil(items.value.length / pageSize.value)
        if (currentPage.value < totalPage)
            currentPage.value = currentPage.value + 1
    }

    const previousStep = () => {
        if (currentPage.value > 0) currentPage.value = currentPage.value - 1
    }
</script>

<template>
    <Story>
        <Variant title="BaseList">
            <BaseList :items="itemsOfCurrentPage" />
            <div class="text-center">
                <BaseButton @click="previousStep">-</BaseButton>
                <BaseButton @click="nextStep">+</BaseButton>
            </div>
        </Variant>
    </Story>
</template>

<style scoped></style>
