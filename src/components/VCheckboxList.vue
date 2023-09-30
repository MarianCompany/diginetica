<script>
import {defineComponent} from 'vue'
import VInput from "./VInput.vue";
import SearchSm from "./icons/SearchSm.vue";
import VCheckbox from "./VCheckbox.vue";

export default defineComponent({
    name: "VCheckboxList",
    components: {VCheckbox, SearchSm, VInput},
    emits: ['update:model-value'],
    props: {
        modelValue: {
            type: Array,
            required: true,
        },

        isWithSearch: {
            type: Boolean,
            default: false,
        },

        checkboxList: {
            type: Array,
            required: true,
        }
    },

    data: function () {
        return {
            searchQuery: '',
        }
    },

    computed: {
        selectedCheckboxesID() {
            return this.modelValue.map((el) => el.id);
        },

        filteredCheckboxList() {
            if (this.searchQuery) {
                return this.checkboxList.filter((el) => {
                    return el.label.toLowerCase().startsWith(this.searchQuery.toLowerCase()) || el.label.toLowerCase().endsWith(this.searchQuery.toLowerCase());
                });
            } else {
                return this.checkboxList;
            }
        },

        isNoResultsBySearch() {
            return this.isWithSearch && this.filteredCheckboxList.length === 0;
        }
    },

    methods: {
        onCheckboxToggle (checkbox, value) {
            if (value && this.selectedCheckboxesID.indexOf(checkbox.id) === -1) {
                this.$emit('update:model-value', [...this.modelValue, checkbox]);
            } else if (!value && this.selectedCheckboxesID.indexOf(checkbox.id) !== -1) {
                const checkboxIndex = this.selectedCheckboxesID.indexOf(checkbox.id);
                const result = [...this.modelValue];

                result.splice(checkboxIndex, 1);

                this.$emit('update:model-value', result);
            }
        }
    }
})
</script>

<template>
    <div class="checkbox-list">
        <div v-if="isWithSearch" class="checkbox-list__search">
            <VInput v-model="searchQuery" :is-search="true" :placeholder="'Поиск'" class="input_padding-xl">
                <div class="input__prefix-img-wrap">
                    <SearchSm class="input__prefix-img"/>
                </div>
            </VInput>
            <p v-if="isNoResultsBySearch" class="checkbox-list__search-msg">
                По вашему запросу ничего не найдено
            </p>
        </div>
        <div v-if="!isNoResultsBySearch" class="checkbox-list__content">
            <TransitionGroup>
                <div
                    v-for="(checkbox, idx) in filteredCheckboxList"
                    :key="checkbox.label + idx"
                    class="checkbox-list__el"
                >

                    <VCheckbox
                            :checked="selectedCheckboxesID.indexOf(checkbox.id) !== -1"
                            :checkbox="checkbox"
                            @update:checked="onCheckboxToggle(checkbox, $event)"
                    />
                    <p class="checkbox-list__el-amount">
                        {{ checkbox.amount }}
                    </p>
                </div>
            </TransitionGroup>
        </div>
    </div>

</template>

<style scoped>
.v-enter-active,
.v-leave-active {
    transition: opacity 0.1s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>