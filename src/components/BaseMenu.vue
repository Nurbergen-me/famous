<template>
  <ul class="menu">
    <li v-for="menuItem in menu" :key="menuItem.title">
        <a class="menu__item" :href="menuItem.link">
            {{ menuItem.title }}
        </a>
    </li>
</ul>
</template>

<script setup>
const props = defineProps(['menu'])

</script>

<style lang="scss" scoped>
.menu {
    margin-left: 48px;
    margin-right: auto;
    padding: 0;
    list-style: none;
    display: flex;
    align-items: center;
    gap: 48px;

    &__item {
        color: #555555;
        text-decoration: none;
    }
}

@media screen and (max-width: 1260px) {
    .menu {
        gap: 24px;
        margin-left: 24px;
    }
}

@media screen and (max-width: 990px) {
    .menu {
        display: none;
    }
}
</style>