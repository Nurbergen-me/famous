<template>
  <header class="header">
    <div class="container header__wrapper">
        <img src="/assets/logo.svg" alt="logo">
        <BaseMenu :menu="menu" />
        <form class="header__form" action="">
            <input type="text" class="header__form-input" placeholder="Поиск по названию картины">
            <BaseButton>
                Найти
            </BaseButton>
        </form>
    </div>
  </header>
</template>

<script setup>
import BaseButton from './BaseButton.vue';
import BaseMenu from './BaseMenu.vue';

const menu = [
        {
            title: 'Каталог',
            link: '#'
        },
        {
            title: 'Доставка',
            link: '#'
        },
        {
            title: 'Оплата',
            link: '#'
        },
        {
            title: 'Контакты',
            link: '#'
        },
        {
            title: 'О галерее',
            link: '#'
        }
    ]
</script>

<style lang="scss" scoped>
.header {
    border-bottom: 1px solid #E1E1E1;
    padding: 24px 0;

    &__wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    &__form {
        display: flex;
        align-items: center;

        &-input {
            font-family: 'Merriweather', serif;
            border: 1px solid #E1E1E1;
            height: 48px;
            padding-left: 16px;
            width: 294px;
        }
    }
}

</style>