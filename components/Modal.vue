<template>
    <div class="modal">
        <div class="modal__outside"></div>
        <div class="modal__container">
            <div class="modal__body">
                <slot></slot>
            </div>
            <div class="modal__footer">
                <slot name="footer"></slot>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.modal {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    min-width: 100vw;
    min-height: 100vh;
    display: flex;
    z-index: 9999;

    &__outside {
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        background-color: #000;
        opacity: 0.5;
    }

    &__container {
        display: flex;
        flex-direction: column;
        gap: 20px;
        margin: auto;
        padding: 20px;
        background-color: #1a1d24;
        min-width: 280px;
        min-height: 150px;
        z-index: 5;
    }
}
</style>
