<template>
    <nav class="nav">
        <ul class="nav-list">
            <li class="nav-list__item">
                <NuxtLink active-class="active" class="nav-list__link" to="/"
                    >Главная</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <NuxtLink class="nav-list__link" to="/exercise-one"
                    >Задание 1</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <NuxtLink class="nav-list__link" to="/exercise-two"
                    >Задание 2</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <NuxtLink class="nav-list__link" to="/exercise-three"
                    >Задание 3</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <button class="nav-list__button btn">Sign up</button>
            </li>
        </ul>
    </nav>
</template>

<style scoped lang="scss">
.nav-list {
    display: flex;
    align-items: center;

    &__item {
        margin-right: 10px;
        margin-left: 10px;

        &:first-child {
            margin-left: 0;
        }

        &:last-child {
            margin-right: 0;
        }
    }

    &__link {
        color: #fff;
        opacity: 0.8;
        padding: 5px;

        &:hover {
            opacity: 1;
        }
    }

    &__button {
        background-color: #7a7a7a;
        color: #fff;
    }
}
</style>
