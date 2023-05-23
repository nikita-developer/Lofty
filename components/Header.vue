<template>
    <header class="header">
        <div class="header__container container">
            <Nav class="header__nav" />
        </div>
    </header>
</template>

<style scoped lang="scss">
.header {
    padding: 10px 15px;
    background-color: #393e48;

    &__container {
        display: flex;
    }

    &__nav {
        margin-left: auto;

        @media (max-width: 768px) {
            margin-left: 0;
            width: 100%;
        }
    }
}
</style>
