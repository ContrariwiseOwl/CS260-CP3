<template>
<div>
    <PoetryList :poems="poems" />
</div>
</template>

<script>
import PoetryList from '@/components/PoetryList'

export default {
    name: 'MyPoetry',
    components: {
        PoetryList,
    },
    mounted() {
        this.id = this.$root.$data.poems.length + 1;
    },
    data() {
        return {
            userName: '',
            title: '',
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
        logIn(userName) {
            this.userName = userName;
        },
        addPoem() {
            this.$root.$data.poems.push({
                id: this.id,
                title: this.title,
                content: this.lines,
                author: this.userName,
                form: this.form
            });
        }
    }
}
</script>