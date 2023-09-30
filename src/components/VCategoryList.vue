<script>
import {defineComponent} from 'vue'

export default defineComponent({
    name: "VCategoryList",
    props: {
        categoryList: {
            type: Array,
            required: true,
        },
    },
})
</script>

<template>
    <div class="category-list">
        <div
            v-for="(category, idx) in categoryList"
            :key="category.name + idx"
            :class="{
                'category_active': category.isActive,
            }"
            class="category"
        >
            <div class="category__wrap">
                <p class="category__name">
                    {{ category.name }}
                </p>
                <p class="category__amount">
                    {{ category.amount }}
                </p>
            </div>
            <div v-if="category.isNested" class="category-list category__category-list">
                <VCategoryList
                    :category-list="category.children"
                />
            </div>
        </div>
    </div>
</template>