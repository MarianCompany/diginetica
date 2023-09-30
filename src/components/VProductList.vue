<script>
import VProductItem from "@/components/VProductItem.vue";
import {defineComponent} from 'vue'

export default defineComponent({
    name: "VProductList",
    components: {
        VProductItem,
    },
    data: function () {
        return {
            products: [
                {
                    brand: 'Бренд',
                    name: 'Полное название товара в несколько строк для вида с обрывом в конце...',
                    price: 5990,
                    oldPrice: 5990,
                    discountPercent: 25,
                    isAvailable: true,
                    isBestseller: true,
                },
                {
                    brand: 'Бренд',
                    name: 'Полное название товара в несколько строк для вида с обрывом в конце...',
                    price: 5990,
                    oldPrice: 5990,
                    discountPercent: 25,
                    isAvailable: true,
                    isBestseller: true,
                },
                {
                    brand: 'Бренд',
                    name: 'Полное название товара в несколько строк для вида с обрывом в конце...',
                    price: 5990,
                    oldPrice: 5990,
                    discountPercent: 25,
                    isAvailable: false,
                    isBestseller: true,
                },
                {
                    brand: 'Бренд',
                    name: 'Полное название товара в несколько строк для вида с обрывом в конце...',
                    price: 5990,
                    oldPrice: 5990,
                    discountPercent: 25,
                    isAvailable: true,
                    isBestseller: true,
                },
                {
                    brand: 'Бренд',
                    name: 'Полное название товара в несколько строк для вида с обрывом в конце...',
                    price: 5990,
                    oldPrice: 5990,
                    discountPercent: 25,
                    isAvailable: true,
                    isBestseller: true,
                },
                {
                    brand: 'Бренд',
                    name: 'Полное название товара в несколько строк для вида с обрывом в конце...',
                    price: 5990,
                    oldPrice: 5990,
                    discountPercent: 25,
                    isAvailable: true,
                    isBestseller: true,
                },
            ],
        }
    }
})
</script>

<template>
    <div class="product-list">
        <VProductItem
            v-for="(product, idx) in products"
            :product-item="product"
            :key="product.name + idx"
        />
    </div>
</template>