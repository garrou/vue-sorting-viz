<template>
    <h1>Vue Sorting Viz</h1>

    <button @click="insertionSort">Insertion sort</button>
    <button @click="bubbleSort">Bubble sort</button>
    <button @click="fillArray">Shuffle</button>

    <div class="container">
        <span class="bar" v-for="(number, index) in array" :key="index" :style="{ height: `${number / 1.5}px` }" />
    </div>
</template>

<script lang="ts" setup>

import { onBeforeMount, ref } from 'vue';

const size = ref<number>(40);
const array = ref<number[]>([])

const fillArray = (): void => {
    array.value = [];

    for (let i = 0; i < size.value; i++) {
        array.value.push(getRandInt(5, 590));
    }
}

const getRandInt = (min: number, max: number): number => {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

const insertionSort = async (): Promise<void> => {
    for (let i = 1; i < size.value; i++) {
        let elt = array.value[i];
        let place;

        for (place = i; place > 0 && array.value[place - 1] > elt; place--) {
            array.value[place] = array.value[place - 1];
        }
        array.value[place] = elt;
        await sleep();
    }
}

const bubbleSort = async (): Promise<void> => {
    let swapped = true

    while (swapped) {
        swapped = false

        for (let i = 0; i < array.value.length - 1; i++) {
            if (array.value[i] > array.value[i + 1]) {
                [array.value[i], array.value[i + 1]] = [array.value[i + 1], array.value[i]]
                await sleep();
                swapped = true
            }
        }
    }
}

const sleep = (): Promise<void> => {
    return new Promise((resolve) => setTimeout(resolve, 20));
}

onBeforeMount(() => {
    fillArray();
})
</script>

<style>
#app {
    text-align: center;
    color: #2c3e50;
}

button {
    margin-right: 5px;
}

.container {
    margin-top: 2%;
    position: fixed;
    left: 50px;
}

.bar {
    width: 20px;
    background-color: black;
    display: inline-block;
    margin: 0 4px;
}
</style>