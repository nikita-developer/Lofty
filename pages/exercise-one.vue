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
        <Modal>
            <div class="exercise-modal">
                <input
                    type="text"
                    class="exercise-modal__field"
                    placeholder="USERNAME"
                />
                <input
                    type="text"
                    class="exercise-modal__field"
                    placeholder="PASSWORD"
                />
            </div>
            <template #footer>
                <div class="exercise-modal__footer">
                    <button class="exercise-modal__button btn">Send</button>
                </div>
            </template>
        </Modal>
    </div>
</template>

<style scoped lang="scss">
.exercise-one {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-auto-rows: minmax(100px, 1fr);
    grid-gap: 20px;
    padding: 20px;

    &__item {
        background-color: #c4c4c4;
    }
}
</style>
