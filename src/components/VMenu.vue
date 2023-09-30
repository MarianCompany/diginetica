<script>
import {defineComponent} from 'vue'
import VCategory from "@/components/VCategoryList.vue";
import VPriceRange from "@/components/VPriceRange.vue";
import VInput from "@/components/VInput.vue";
import VCheckboxList from "@/components/VCheckboxList.vue";

export default defineComponent({
    name: "VMenu",
    components: {
        VCheckboxList,
        VInput,
        VPriceRange,
        VCategory
    },
    data: function () {
        return {
            categories: [
                {
                    name: 'Название категории',
                    amount: 3,
                    isActive: false,
                    isNested: true,
                    children: [
                        {
                            name: 'Название категории',
                            amount: 3,
                            isActive: false,
                            isNested: false,
                        },
                        {
                            name: 'Название категории',
                            amount: 3,
                            isActive: false,
                            isNested: false,
                        },
                        {
                            name: 'Название категории',
                            amount: 3,
                            isActive: true,
                            isNested: false,
                        },
                    ]
                }
            ],
            price: {
                from: 0,
                to: 9999,
            },
            brands: {
                options: [
                    {
                        id: 0,
                        label: 'Атрибут1',
                        amount: 3,
                    },
                    {
                        id: 1,
                        label: 'Атрибут2',
                        amount: 3,
                    },
                    {
                        id: 2,
                        label: 'Атрибут3',
                        amount: 3,
                    },
                    {
                        id: 3,
                        label: 'Атрибут4',
                        amount: 3,
                    },
                    {
                        id: 4,
                        label: 'Атрибут5',
                        amount: 3,
                    },
                    {
                        id: 5,
                        label: 'Атрибут6',
                        amount: 3,
                    },
                    {
                        id: 6,
                        label: 'Атрибут7',
                        amount: 3,
                    },
                    {
                        id: 7,
                        label: 'Атрибут8',
                        amount: 3,
                    },
                ],
                result: [],
            },
            sizes: {
                options: [
                    {
                        id: 0,
                        label: 'Атрибут1',
                        amount: 3,
                    },
                    {
                        id: 1,
                        label: 'Атрибут2',
                        amount: 3,
                    },
                    {
                        id: 2,
                        label: 'Атрибут3',
                        amount: 3,
                    },
                    {
                        id: 3,
                        label: 'Атрибут4',
                        amount: 3,
                    },
                    {
                        id: 4,
                        label: 'Атрибут5',
                        amount: 3,
                    },
                    {
                        id: 5,
                        label: 'Атрибут6',
                        amount: 3,
                    },
                ],
                result: [],
            },
        }
    },
    methods: {
        clearCheckboxList (checkboxListName) {
            this[checkboxListName].result.length = 0;
        }
    }
})
</script>

<template>
    <div class="menu">
        <div class="menu__item">
            <div class="menu__item-content">
                <VCategory :category-list="categories" />
            </div>
        </div>
        <div class="menu__item">
            <div class="menu__item-header">
                <h4 class="title">
                    Цена
                </h4>
            </div>
            <div class="menu__item-content">
                <VPriceRange />
            </div>
        </div>
        <div class="menu__item">
            <div class="menu__item-header menu__item-header_space-between">
                <h4 class="title">
                    Бренд
                </h4>
                <a class="menu__link" @click="clearCheckboxList('brands')">
                    Очистить
                </a>
            </div>
            <div class="menu__item-content">
                <VCheckboxList
                    v-model="brands.result"
                    :checkbox-list="brands.options"
                    :is-with-search="true"
                />
            </div>
        </div>
        <div class="menu__item">
            <div class="menu__item-header">
                <h4 class="title">
                    Размер
                </h4>
            </div>
            <div class="menu__item-content">
                <VCheckboxList
                    v-model="sizes.result"
                    :checkbox-list="sizes.options"
                />
            </div>
        </div>
    </div>
</template>