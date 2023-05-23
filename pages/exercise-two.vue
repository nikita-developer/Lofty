<template>
    <div class="exercise">
        <h1 class="exercise__title">Задание 2</h1>
        <h4 class="exercise__subtitle">Переписать Promise на Async/Await</h4>
        <hr>
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
    </div>
</template>

<style lang="scss" scoped>
    .exercise-two {
        padding: 20px 40px;
        background-color: #1e2431;
        color: #fff;

        &:last-child {
            margin-top: 40px;
        }
    }
</style>