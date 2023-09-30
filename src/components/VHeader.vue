<script>
import {defineComponent} from 'vue'
import VSearch from "./VSearch.vue";
import Pointer from "./icons/Pointer.vue";
import Logo from "./icons/Logo.vue";

export default defineComponent({
    name: "VHeader",
    components: {Logo, Pointer, VSearch},
    data: function () {
        return {
            searchQuery: '',
        }
    }
})
</script>

<template>
    <header class="header">
        <div class="container">
            <div class="header__wrapper">
                <div class="header__block header__block_desktop">
                    <div class="header__logo-wrap">
                        <div class="logo">
                            <Logo class="logo__img" />
                            <p class="logo__text">
                                Логотип
                            </p>
                        </div>
                    </div>
                    <div class="header__label-wrap">
                        <div class="header__label">
                            <p class="header__label-text">
                                Каталог
                            </p>
                        </div>
                    </div>
                </div>
                <div class="header__block header__search-block">
                    <div class="header__search-wrap">
                        <Pointer class="header__search-pointer" />
                        <VSearch v-model="searchQuery" :placeholder="'Поиск по 100 000 товаров'" />
                    </div>

                </div>
                <div class="header__block header__block_desktop">
                    <nav class="nav header__nav">
                        <a class="nav__link">
                            Информация о компании
                        </a>
                        <a class="nav__link">
                            Контакты
                        </a>
                        <a class="nav__link">
                            Полезные ссылки
                        </a>
                    </nav>
                </div>
            </div>
        </div>
    </header>
</template>