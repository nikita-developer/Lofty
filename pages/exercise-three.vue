<template>
    <div class="exercise">
        <h1>Задание 3</h1>
        <h4 class="exercise__subtitle">
            Реализовать функцию для кэширования результата выполнения
            асинхронной функции
        </h4>
        <h4 class="exercise__subtitle">
            <small>Первый аргумент - асинхронная функция</small>
        </h4>
        <h4 class="exercise__subtitle">
            <small>Второй аргумент - время кэша в секундах</small>
        </h4>
        <hr />
        <div class="exercise__body">
            <div class="exercise-three">
                <pre>
let count = 0;

const getData = () => Promise.resolve(++count)
const sleep = (n) => new Promise(resolve => setTimeout(resolve, n))

const getJsonMemoize = memoize(getData, 1000)

await getJsonMemoize() // 1
await getJsonMemoize() // 1
await sleep(3000)
await getJsonMemoize() // 2
                </pre>
            </div>
        </div>
        <h4 class="exercise__subtitle">Результат:</h4>
        <hr />
        <div class="exercise__body">
            <div class="exercise-three">
                <pre>
let count = 0

const getData = () => Promise.resolve(++count)
const sleep = (n) => new Promise((resolve) => setTimeout(resolve, n))

const memoize = (func, time) => {
    func()
    setTimeout(() => func(), time)
    return () => console.log(count)
}

const getJsonMemoize = memoize(getData, 1000)

await getJsonMemoize() // 1
await getJsonMemoize() // 1
await sleep(3000)
await getJsonMemoize() // 2
                </pre>
            </div>
        </div>
    </div>
</template>

<script setup>
let count = 0

const getData = () => Promise.resolve(++count)
const sleep = (n) => new Promise((resolve) => setTimeout(resolve, n))

const memoize = (func, time) => {
    func()
    setTimeout(() => func(), time)
    return () => console.log(count)
}

const getJsonMemoize = memoize(getData, 1000)

// await getJsonMemoize() // 1
// await getJsonMemoize() // 1
// await sleep(3000)
// await getJsonMemoize() // 2
</script>

<style lang="scss" scoped>
.exercise-three {
    padding: 20px 40px;
    background-color: #1e2431;
    color: #fff;

    @media (max-width: 768px) {
        padding: 15px;
    }

    pre {
        overflow-x: auto;
    }

    &:first-child {
        margin-bottom: 40px;
    }
}
</style>
