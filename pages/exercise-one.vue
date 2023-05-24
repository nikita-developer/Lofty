<template>
    <div class="exercise">
        <h1>Задание 1</h1>
        <h4 class="exercise__subtitle">
            Адаптивную сетку: Десктоп 3 блока, планшет 2, мобильные девайсы 1
        </h4>
        <h4 class="exercise__subtitle">
            Модальное окно при клике на кнопку sign up
        </h4>
        <h4 class="exercise__subtitle">
            AJAX обработчик для формы в модальном окне (отправить POST запрос)
        </h4>
        <hr />
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

    @media (max-width: 480px) {
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    }

    &__item {
        background-color: #c4c4c4;
    }
}
</style>
