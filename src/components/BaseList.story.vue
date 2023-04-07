<script setup>
    import { ref, computed } from "vue"

    const items = ref(["a", "b", "c", "d", "e", "f"])
    const pageSize = 3
    const currentPage = ref(0)

    const itemsOfCurrentPage = computed(() => {
        const begin = currentPage.value * pageSize
        return items.value.slice(begin, begin + 3)
    })

    function nextStep() {
        const totalPage = Math.ceil(items.value.length / pageSize) - 1
        if (currentPage.value < totalPage) currentPage.value += 1
    }

    function previousStep() {
        if (currentPage.value > 0) currentPage.value -= 1
    }
</script>

<template>
    <Story>
        <Variant title="BaseList">
            <div>
                <BaseList :items="items" />
            </div>
        </Variant>
        <Variant title="PaginatedBaseList">
            <div>
                <BaseList :items="itemsOfCurrentPage" />
                <div class="text-center">
                    <BaseButton @click="previousStep">-</BaseButton>
                    <BaseButton @click="nextStep">+</BaseButton>
                </div>
            </div>
        </Variant>
    </Story>
</template>

<style scoped></style>
