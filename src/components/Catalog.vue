<template>
  <section class="catalog">
    <div class="container">
        <h1 class="catalog__title">
            Картины эпохи Возрождения
        </h1>
        <div class="catalog__items">
            <div 
                v-for="picture in pictures" 
                class="catalog__item" 
                :class="!picture.onSale ? 'sold' : ''"
                :key="picture.id">
                <img :src="`/assets/${picture.image}`" class="catalog__item-img" alt="picture">
                <h2 class="catalog__item-name">
                    {{ picture.title }}
                </h2>
                <div class="catalog__item-footer" v-if="picture.onSale">
                    <div class="catalog__item-price">
                        <span class="old-price" v-if="picture.oldPrice">
                            {{ picture.oldPrice }} $
                        </span>
                        <span class="new-price">
                            {{ picture.newPrice }} $
                        </span>
                    </div>
                    <BaseButton 
                        :loading="isLoading(picture.id)"
                        :inCart="isInCart(picture.id)"
                        @click="addToCart(picture)"
                        >
                        Купить
                    </BaseButton>
                </div>
                <div class="catalog__item-footer" v-else>
                    <div class="catalog__item-sold">
                        Продана на аукционе
                    </div>
                </div>
            </div>
        </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, inject, onMounted } from 'vue'
import BaseButton from './BaseButton.vue'

const axios = inject('axios') 
const pictures = [
    {
        id: 1,
        image: 'product-1.jpg',
        title: '«Рождение Венеры» Сандро Боттичелли',
        newPrice: '1 000 000',
        oldPrice: '2 000 000',
        onSale: true
    },
    {
        id: 2,
        image: 'product-2.jpg',
        title: '«Тайная вечеря»  Леонардо да Винчи',
        newPrice: '3 000 000',
        oldPrice: null,
        onSale: true
    },
    {
        id: 3,
        image: 'product-3.jpg',
        title: '«Сотворение Адама» Микеланджело',
        newPrice: '5 000 000',
        oldPrice: '6 000 000',
        onSale: true
    },
    {
        id: 4,
        image: 'product-4.jpg',
        title: '«Урок анатомии»  Рембрандт',
        newPrice: '1 000 000',
        oldPrice: '2 000 000',
        onSale: false
    },
]

const catalog = reactive({
    loading: false,
    currentPicture: null,
    cart: []
})

onMounted(() => {
    if (localStorage.cart) {
        catalog.cart = localStorage.cart.split(',')
    }
})

function isInCart(id) {
    return catalog.cart.find((cartItem) => Number(cartItem) === id)
}

function isLoading(id) {
    return catalog.loading && catalog.currentPicture === id
}

function addToCart(picture) {
    if (isInCart(picture.id)) return
    catalog.loading = true
    catalog.currentPicture = picture.id
    axios.get('https://jsonplaceholder.typicode.com/posts/1')
        .then((res) => {
            catalog.loading = false
            catalog.currentPicture = null
            catalog.cart.push(picture.id)

            localStorage.cart = catalog.cart
        })
}

</script>

<style lang="scss" scoped>
.catalog {
    padding: 45px 0 90px;

    &__title {
        margin-bottom: 39px;
    }

    &__items {
        display: flex;
        flex-wrap: wrap;
        gap: 26px;
    }

    &__item {
        border: 1px solid #E1E1E1;
        width: 280px;
        display: flex;
        flex-direction: column;

        &.sold {
            opacity: 0.5;
        }

        &-img {
            width: 100%;
            height: 160px;
            object-fit: cover;
        }

        &-name {
            padding: 20px 24px 23px;
        }

        &-footer {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-top: auto;
            padding: 0 24px 24px;
        }

        &-price {
            color: black;
            .old-price {
                font-weight: 300;
                font-size: 14px;
                line-height: 150%;
                text-decoration-line: line-through;
                color: #A0A0A0;
            }

            .new-price {
                display: block;
                font-weight: 700;
                font-size: 16px;
                line-height: 150%;
            }
        }

        &-sold {
            font-weight: 700;
            line-height: 48px;
        }
    }
}
</style>