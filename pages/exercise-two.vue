<template>
    <div class="exercise">
        <h1>Задание 2</h1>
        <h4 class="exercise__subtitle">Переписать Promise на Async/Await</h4>
        <hr />
        <div class="exercise__body">
            <div class="exercise-two">
                <pre>
const getJson = url => fetch(url).then(res => res.json());

getJson('/i/1.json')
.then(json => {
    if (json.key) {
        return getJson('/i/2.json')
    }
    throw new Error('No key')
})
.then(json => {
    return json.key2
})
.catch(error => {
    console.error(error)
})
                </pre>
            </div>
        </div>
        <h4 class="exercise__subtitle">Результат:</h4>
        <hr />
        <div class="exercise__body">
            <div class="exercise-two">
                <pre>
const getJson = async (url) => {
    try {
        const res = await fetch(url)
        const json = await res.json()

        if (json.key) return getJson('/i/2.json')

        if (json) return json.key2

        throw new Error('No key')
    } catch (error) {
        console.error(error)
    }
}

getJson('/i/1.json')
                </pre>
            </div>
        </div>
    </div>
</template>

<script setup>
const getJson = async (url) => {
    try {
        const res = await fetch(url)
        const json = await res.json()

        if (json.key) return getJson('/i/2.json')

        if (json) return json.key2

        throw new Error('No key')
    } catch (error) {
        console.error(error)
    }
}

// getJson('/i/1.json')
</script>

<style lang="scss" scoped>
.exercise-two {
    padding: 20px 40px;
    background-color: #1e2431;
    color: #fff;

    &:first-child {
        margin-bottom: 40px;
    }
}
</style>
