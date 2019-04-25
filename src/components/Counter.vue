<template>
    <div class="counter">
        <h1>Counter</h1>
        <div class="count">{{ count }}</div>
        <button @click="decreaseCount">---</button> <button @click="increaseCount">+++</button>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Counter extends Vue {
    
    count: number = 0;

    public increaseCount(): void {
        this.count++;
    }
    public decreaseCount(): void {
        this.count--;
    }
}
</script>

