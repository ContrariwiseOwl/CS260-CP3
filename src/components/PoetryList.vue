<template>
    <div>
        <div class="poem" v-for="poem in poems" :key="poem.id">
            <p><strong>{{poem.title}}</strong> by {{poem.author}}</p>
            <div class="stanza">
                <ul>
                    <li v-for="line in poem.content" :key="line.charAt(0)">{{line}}</li>
                </ul>
            </div>
        </div>
    </div>             
</template>

<script>
export default {
    name: 'PoetryList',
    props: {
        poems: Array
    },
}
</script>

<style scoped>
.poem {
    padding: 6px 12px;
}
</style>