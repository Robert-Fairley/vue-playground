<template>

    <div>
        <h1>{{ componentTitle }}</h1>

        <div class="a-cont">
            <pre class="raw">{{displayDoc()}}</pre>
            <div class="draggable">
                <div>
                    <small>title</small>
                    <br/>
                    <strong class="dat">{{data.title}}</strong>
                </div>
                <div>
                    <small>version</small>
                    <br/>
                    <span class="dat">{{ data.version }}</span>
                </div>
                <div>
                    <div>
                        <small>
                            excerpt
                        </small>
                        <br/>
                        <span class="dat">{{data.metadata.excerpt}}</span>
                    </div>
                </div>
                <vue-nestable v-model="data.components">
                    <vue-nestable-handle
                        slot-scope="{ item }"
                        :item="item"
                    >
                        <div>
                            <small class="dra">{{ item.role }}</small>
                            <br/>
                            <span class="dat">{{ item.text }}</span>
                        </div>
                    </vue-nestable-handle>
                </vue-nestable>
            </div>
        </div>

        <hr/>
        <form>
            <label>
                Title: <input type="text" :value="data.title" @input="updateTitle" />
            </label>
            <label>
                Role: <input type="text" :value="field.role" @input="updateFieldRole" />
                Text: <input type="text" :value="field.text" @input="updateFieldText" />
                <button @click="addComponent">Add</button>
            </label>
        </form>
    </div>
</template>

<style>
.a-cont {
    display: flex;
    justify-content: space-around;
    align-content: flex-start;
}

small {
    background: #efefef;
    padding: 0.25em;
    color: #333;
}
.dra {
    cursor:ns-resize;
}
.dat {
    padding: 0.5em;
    margin: 1em;
}

.raw {
    margin: 0;
    border: 1px solid #ccc;
    background: #efefef;
    border-radius: 8px;
    padding: 1em;
    width: 46%;
    text-align: left;
    vertical-align: top;
}
.draggable {
    vertical-align: top;
    padding: 1em;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: 46%;
    text-align: left;
}
</style>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { Document } from "./document";
import VueNestable from "vue-nestable";

Vue.use(VueNestable);

@Component
export default class Doc extends Vue {

    @Prop() private componentTitle!: string;

    public data: Document = {
        title: "",
        version: "1.9",
        metadata: {
            excerpt: "testing testing testing testing",
        },
        components: [],
    };

    public field = {
        role: "",
        text: "",
    }

    public updateTitle(evt: any): void {
        this.data.title = evt.target.value;
    }

    public updateFieldRole(evt: any): void {
        this.field.role = evt.target.value;
    }

    public updateFieldText(evt: any): void {
        this.field.text = evt.target.value;
    }

    public addComponent(evt: any, role: string, text: string): void {
        evt.preventDefault();

        this.data.components.push({
            id: this.componentId(),
            role: this.field.role,
            text: this.field.text,
        });
        this.field.role = "";
        this.field.text = "";
    }

    public displayDoc(): string {
        return JSON.stringify(this.data, null, 2);
    }

    private componentId(): string {
        return `comp_${Math.floor(Math.random() * Date.now())}`;
    }
}

</script>
