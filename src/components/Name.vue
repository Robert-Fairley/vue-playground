<template>
    <section class="names">
        <div style="margin: 2em;">
            Hi there, {{pName}}
        </div>
        <div>
            So far, I've met:
            <br/>
            <span class="list">
                {{listNames()}}
            </span>
        </div>
        <div id="form">
            <input type="text" :value="pName" @input="updateName"/> <button @click="add">Add Name</button>
        </div>
    </section>
</template>

<style>
.names {
    margin: 2em;
    border-top: 2px solid #bbb;
}

input[type="text"] {
    padding: 0.5em;
    font-size: 1.5em;
    font-weight: 100;
    color: #333;
}

</style>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Name extends Vue {

    pName: string = "...wait, what's your name again?";
    names: string[] = [];

    public updateName(evt: any): void {
        this.pName = evt.target.value;
    }

    public add(): void {
        this.names.push(`${this.pName}`);
    }

    public listNames(): string {
        let out: string | string[] = '';

        for (const name of this.names)
            out += name + ', ';

        out= out.split('');
        delete out[out.length -1];
        delete out[out.length-2];
        out = out.join('');
        return out;
    }
}

</script>
