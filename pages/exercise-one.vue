<template>
    <div class="exercise">
        <h1 class="exercise__title">Задание</h1>
        <div class="exercise__body">
            <div class="exercise-one">
                <div class="exercise-one__item"></div>
                <div class="exercise-one__item"></div>
                <div class="exercise-one__item"></div>
                <div class="exercise-one__item"></div>
                <div class="exercise-one__item"></div>
                <div class="exercise-one__item"></div>
            </div>
        </div>
    </div>
</template>

<script setup></script>

<style scoped lang="scss">
.exercise-one {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-auto-rows: minmax(100px, 1fr);
    grid-gap: 20px;
    padding: 20px;
    border: 5px dashed #fff;

    &__item {
        background-color: #c4c4c4;
    }
}
</style>
