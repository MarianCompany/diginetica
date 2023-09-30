<script>
import {defineComponent} from 'vue'
import CrossCircle from "./icons/CrossCircle.vue";
import Search from "./icons/Search.vue";

export default defineComponent({
    name: "VSearch",
    components: {Search, CrossCircle},
    emits: ['update:model-value'],
    props: {
        modelValue: {
            type: String,
            required: true,
        },
        placeholder: {
            type: String,
            default: 'Запрос',
        }
    },
    data: function () {
        return {
            isInFocus: false,
        }
    },
    methods: {
        updateSearchQuery(e) {
            this.$emit('update:model-value', e.target.value);
        },

        clearQuery() {
            this.$emit('update:model-value', '')
        },

        executeSearch() {
            alert('В разработке :]');
        },

        setIsInFocus(payload) {
            this.isInFocus = payload;
        },
    }
})
</script>

<template>
    <div
        :class="{
            'search_focused': isInFocus,
        }"
        class="search"
    >
        <div class="search__prefix">
            <Search class="search__prefix-img" />
        </div>
        <input
            :value="modelValue"
            :placeholder="placeholder"
            @input="updateSearchQuery"
            @keydown.enter="executeSearch"
            @focus="setIsInFocus(true)"
            @focusout="setIsInFocus(false)"
            type="text"
            class="search__input"
        />
        <div class="search__controls">
            <Transition>
                <CrossCircle v-if="isInFocus" class="search__clear-query" @click="clearQuery" />
            </Transition>
            <button class="btn btn_blue search__btn" @click="executeSearch">
                Найти
            </button>
        </div>
    </div>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
    transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>