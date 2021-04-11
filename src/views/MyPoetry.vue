<template>
<div>
    <div v-if="noName">
        <div id="nameInput">
            <form v-on:submit.prevent="logIn">
                <input type="text" v-model="userName"/>
                <button type="submit">Set User</button>
            </form>
        </div>
    </div>
    <div v-else>
        <div class="poem-input">
            <form v-on:submit.prevent="addPoem">
                <input type="text" v-model="title" placeholder="Poem Title"/>
                <input type="text" v-model="form" placeholder="Poetry Form"/>
                <div class="stanza">
                    <ul>
                        <li v-for="line in lines" :key="line">{{line}}</li>
                    </ul>
                </div>
                <form v-on:submit.prevent="addLine">
                    <input type="text" v-model="newLine" placeholder="Add line to poem"/>
                    <button type="submit">Add Line</button>
                </form>
                <button type="submit">Add Poem</button>
            </form>
        </div>
        <PoetryList :poems="poems" />
    </div>
</div>
</template>

<script>
import PoetryList from '@/components/PoetryList'

export default {
    name: 'MyPoetry',
    components: {
        PoetryList,
    },
    data() {
        return {
            noName: true,
            userName: '',
            title: '',
            newLine: '',
            lines: [],
            form: '',
        }
    },
    computed: {
        poems() {
            return this.$root.$data.poems.filter( poem => poem.author == this.userName);
        },
        id() {
            return this.$root.$data.poems.length + 1;
        }
    },
    methods: {
        logIn() {
            this.noName = false;
        },
        addPoem() {
            this.$root.$data.poems.push({
                id: this.id,
                title: this.title,
                content: this.lines,
                author: this.userName,
                form: this.form
            });
            this.title = '';
            this.lines = [];
            this.form = '';
        },
        addLine() {
            this.lines.push(this.newLine);
            this.newLine = '';
        }
    }
}
</script>

