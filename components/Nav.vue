<template>
    <nav class="nav">
        <ul class="nav-list">
            <li class="nav-list__item">
                <NuxtLink active-class="active" class="nav-list__link" to="/"
                    >Главная</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <NuxtLink
                    active-class="active"
                    class="nav-list__link"
                    to="/exercise-one"
                    >Задание 1</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <NuxtLink
                    active-class="active"
                    class="nav-list__link"
                    to="/exercise-two"
                    >Задание 2</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <NuxtLink
                    active-class="active"
                    class="nav-list__link"
                    to="/exercise-three"
                    >Задание 3</NuxtLink
                >
            </li>
            <li class="nav-list__item">
                <button
                    class="nav-list__button btn"
                    @click="isOpenModal = true"
                >
                    Sign up
                </button>
            </li>
        </ul>
        <Modal :show="isOpenModal" @close="isOpenModal = false">
            <div class="exercise-modal">
                <input
                    type="text"
                    class="exercise-modal__field"
                    placeholder="USERNAME"
                    v-model.trim="login"
                />
                <input
                    type="text"
                    class="exercise-modal__field"
                    placeholder="PASSWORD"
                    v-model.trim="password"
                />
            </div>
            <template #footer>
                <div class="exercise-modal__footer">
                    <button class="exercise-modal__button btn" @click="submit">
                        Send
                    </button>
                </div>
            </template>
        </Modal>
    </nav>
</template>

<script setup>
const isOpenModal = ref(false)
const login = ref('')
const password = ref('')

const submit = async () => {
    const settings = {
        method: 'POST',
        body: JSON.stringify({ login, password }),
        headers: {
            'content-type': 'application/json',
        },
    }
    try {
        const fetchResponse = await fetch(
            `https://jsonplaceholder.typicode.com/posts`,
            settings
        )
        const data = await fetchResponse.json()
        console.log('Post запрос отправлен', data)
        isOpenModal.value = false
    } catch (e) {
        return e
    }
}
</script>

<style scoped lang="scss">
.nav-list {
    display: flex;
    align-items: center;

    @media (max-width: 768px) {
        flex-direction: column;
    }

    &__item {
        margin-right: 5px;
        margin-left: 5px;

        @media (max-width: 768px) {
            margin: 5px 0;
        }

        &:first-child {
            margin-left: 0;
        }

        &:last-child {
            margin-right: 0;
        }
    }

    &__link {
        display: inline-block;
        color: #fff;
        opacity: 0.8;
        padding: 10px 15px;

        &:hover {
            opacity: 1;
        }

        &.active {
            background-color: #1a1d2459;
            opacity: 1;
        }
    }

    &__button {
        background-color: #7a7a7a;
        color: #fff;
    }
}
</style>
