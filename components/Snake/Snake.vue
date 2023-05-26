<template>
    <div class="snake">
        <h4>Поиграем в змейку?</h4>
        <div class="snake-settings snake__settings">
            <div class="snake-settings__row">
                <p class="snake-settings__label">Выберите сложность</p>
                <select 
                    :class="{disabled: activeButton}" 
                    :disabled="activeButton" 
                    class="snake-settings__select"
                    v-model="complexity"
                >
                    <option :value="500" class="snake-settings__option">Легкая</option>
                    <option :value="300" class="snake-settings__option">Средняя</option>
                    <option :value="100" class="snake-settings__option">Тяжелая</option>
                </select>
            </div>
            <div class="snake-settings__row">
                <button 
                    :disabled="activeButton"
                    :class="{disabled: activeButton}"
                    class="snake-settings__button btn" 
                    @click="start"
                >
                    Погнали
                </button>
            </div>
            <div class="snake-settings__row">
                <button 
                    :disabled="!activeButton"
                    :class="{disabled: !activeButton}"
                    class="snake-settings__button btn" 
                    @click="theEnd"
                >
                    Сдаюсь
                </button>
            </div>
        </div>
        <div class="snake__wrap">
            <div class="snake__body">
                <div
                    class="snake__item"
                    v-for="(item, index) in field"
                    :key="index"
                    :class="{
                        active: snake.includes(index) || index === food,
                    }"
                ></div>
            </div>
        </div>
        <Modal :show="isOpenModal" @close="isOpenModal = false">
            <div class="snake__message">
                <h1 >Вы проиграли!</h1>
            </div>
        </Modal>
    </div>
</template>

<script setup>
// сложность
let complexity = ref(500)

// поле
const field = ref(new Array(256))
// змейка
const snake = ref([1, 2, 3])

// рамки поля
const borderTop = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
const borderRight = [15, 31, 47, 63, 79, 95, 111, 127, 143, 159, 175, 191, 207, 223, 239, 255]
const borderBottom = [240, 241, 242, 243, 244, 245, 246, 247, 248, 249, 250, 251, 252, 253, 254, 255]
const borderLeft = [0, 16, 32, 48, 64, 80, 96, 112, 128, 144, 160, 176, 192, 208, 224, 240]

let activeButton = ref(false)

let timer
// модальное окно
const isOpenModal = ref(false)

// рандомная вкусняшка
let food = ref(randomFood())

// направление
const directionRun = ref('ArrowLeft')

const start = () => {
    let foods = []
    activeButton.value = true

    timer = setInterval(() => {
        // запрещаем движение змейки в протвоположное направление
        document.addEventListener('keydown', (event) => {
            if (directionRun.value === 'ArrowUp' && event.key === 'ArrowDown') return
            if (directionRun.value === 'ArrowRight' && event.key === 'ArrowLeft') return
            if (directionRun.value === 'ArrowDown' && event.key === 'ArrowUp') return
            if (directionRun.value === 'ArrowLeft' && event.key === 'ArrowRight') return
            directionRun.value = event.key
        }, {once: true})

        lengthSnake()

        snake.value.filter((number, index, numbers) => {
            if (numbers.indexOf(number) !== index) {
                theEnd()
            } else {
                // если скушали вкусняшку
                if (snake.value[0] === food.value) {
                    foods.push(food.value)
                    food.value = randomFood()
                }

                // када еда дойдет до хвостика, змейка увеличивается
                if (snake.value[snake.value.length - 1] === foods[0]) {
                    snake.value.push(foods[0])
                    foods.splice(0, 1)
                }
            }
        })
    }, complexity.value)
}

const theEnd = () => {
    clearInterval(timer)
    snake.value = [1, 2, 3]
    activeButton.value = false
    isOpenModal.value = true
    directionRun.value = 'ArrowLeft'
}

// хрен пойми что я тут написал но это работает)
// короче, эта функция передает элементам массива змейки значение соседнего элемента
const lengthSnake = () => {
    let oldCount = snake.value[0]
    let newCount = snake.value[0]

    // указываем куда двигаться
    snake.value[0] = direction(directionRun.value)

    for (let i = 1; i < snake.value.length; i++) {
        oldCount = snake.value[i]
        snake.value[i] = newCount
        newCount = oldCount
    }
}

// рандомное число
function randomFood() {
    let count = Math.floor(Math.random() * 256)
    return snake.value.includes(count) ? randomFood() : count
}

// задаем направление
const direction = (directionRun) => {
    // если движемся вверх
    if (directionRun === 'ArrowUp') {
        if (borderTop.includes(snake.value[0])) {
            return (snake.value[0] += borderBottom[0])
        }
        return (snake.value[0] -= 16)
    }

    // если движемся вправо
    if (directionRun === 'ArrowRight') {
        if (borderRight.includes(snake.value[0])) {
            return (snake.value[0] -= borderRight[0])
        }
        return (snake.value[0] += 1)
    }

    // если движемся вниз
    if (directionRun === 'ArrowDown') {
        if (borderBottom.includes(snake.value[0])) {
            return (snake.value[0] -= borderBottom[0])
        }
        return (snake.value[0] += 16)
    }

    // если движемся влево
    if (directionRun === 'ArrowLeft') {
        if (borderLeft.includes(snake.value[0])) {
            return (snake.value[0] += borderLeft.length - 1)
        }
        return (snake.value[0] -= 1)
    }
}
</script>

<style lang="scss" scoped>
.snake {
    max-width: 500px;
    &__wrap {
        position: relative;
        background-color: #000;
        padding-top: 100%;
    }

    &__body {
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            display: grid;
            grid-template-rows: repeat(16, 1fr);
            grid-template-columns: repeat(16, 1fr);
        }

    &__item {
        position: relative;
        color: #fff;
        font-size: 12px;
        outline: 1px solid rgb(255 255 255 / 10%);

        &.active {
            background-color: yellow;
            color: #000;
        }

        & span {
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }
    }
    
    &__settings {
        margin-bottom: 30px;
    }

    &__message {
        width: 260px;
        height: 150px;
        display: flex;
        justify-content: center;
        align-items: center;

        h1 {
            margin-bottom: 0;
        }
    }
}

.snake-settings {
    color: #fff;
    
    &__row {
        & + & {
            margin-top: 15px;
        }
    }

    &__label {
        font-size: 14px;
        margin-bottom: 10px;
    }

    &__select {
        width: 250px;
        padding: 5px;
        border: 1px solid #fff;
        border-radius: 5px;

        &.disabled {
            opacity: .3;
        }
    }

    &__option {
        background-color: #202124;
    }

    &__button {
        border: 1px solid #fff;
        border-radius: 5px;

        &.disabled {
            opacity: .3;
        }
    }
}
</style>
