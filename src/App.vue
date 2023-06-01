<template>
  <h1>Vue Sorting Viz</h1>

  <button @click="insertionSort()">Insertion sort</button>
  <button @click="fillArray()">Shuffle</button>

  <div class="container">
    <span class="bar" v-for="(number, index) in array" :key="index" :style="{ height: `${number / 1.5}px` }" />
  </div>
</template>

<script lang="ts">

interface ArrayData {
  array: number[];
  size: number;
}

export default {
  data(): ArrayData {
    return {
      array: [],
      size: 40
    }
  },
  created(): void {
    this.fillArray();
  },
  methods: {
    fillArray(): void {
      this.array = [];

      for (let i = 0; i < this.size; i++) {
        this.array.push(this.getRandInt(5, 590));
      }
    },
    getRandInt(min: number, max: number): number {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    async insertionSort(): Promise<void> {
      for (let i = 1; i < this.size; i++) {
        let elt = this.array[i];
        let place;

        for (place = i; place > 0 && this.array[place - 1] > elt; place--) {
          this.array[place] = this.array[place - 1];
        }
        this.array[place] = elt;
        await this.sleep();
      }
    },
    sleep(): Promise<void> {
      return new Promise((resolve) => setTimeout(resolve, 100));
    }
  }
}
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
  position: fixed;
  left: 50px;
  margin-top: 20px;
}

.bar {
  width: 20px;
  background-color: black;
  display: inline-block;
  margin: 0 4px;
}
</style>
