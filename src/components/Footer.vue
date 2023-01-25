<template>
  <footer class="footer">
    <div class="container footer__wrapper">
        <img src="/assets/logo-footer.svg" alt="logo">
        <BaseMenu :menu="menu" />
        <div class="footer__contacts">
            <div class="footer__contacts-item">
                <img src="/assets/phone-icon.svg" alt="phone">
                <a href="tel:+74955555555" class="text">
                    +7 (495) 555-55-55
                </a>
            </div>
            <div class="footer__contacts-item">
                <img src="/assets/location-icon.svg" alt="phone">
                <div class="text">
                    г. Москва, ул. Расплетина, 24
                </div>
            </div>
        </div>
    </div>
  </footer>
</template>

<script setup>
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
.footer {
    background: #ECEAEA;
    padding: 24px 0;
    margin-top: auto;

    &__wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    &__contacts {
        display: flex;
        align-items: center;
        gap: 51px;

        &-item {
            display: flex;
            align-items: center;
            gap: 9px;

            .text {
                font-size: 14px;
                color: #555555;
                text-decoration: none;
            }
        }
    }
}

@media screen and (max-width: 560px) {
    .footer {
        &__wrapper {
            flex-direction: column;
        }

        &__contacts {
            flex-direction: column;
            margin-top: 30px;
            gap: 20px;
        }
    }
}
</style>