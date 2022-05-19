<script lang="ts">
import { onMounted, ref, watch, toRefs, computed } from 'vue';
// defineProps<{ msg: string }>();

export default {
    props: {
        msg: {
            type: String,
            default: '',
        },
    },
    setup(props) {
        const { msg } = toRefs(props);
        const count = ref(2);
        let twiceTheCounter = ref(count);
        twiceTheCounter = computed(() => count.value * 2);
        console.log(count.value, '看看count');
        const clgTime = () => {
            setTimeout(() => {
                console.log('执行clgTime');
            }, 2000);
        };
        onMounted(clgTime);
        watch(count, (newVal, oldVal) => {
            console.log(newVal, oldVal, '看看watch------------');
            msg.value = 'Jimous is cool';
        });
        watch(msg, (newVal, oldVal) => {
            console.log('msg update-----', newVal);
        });
        return {
            twiceTheCounter,
            count,
            clgTime,
        };
    },
    watch: {
        count(val) {
            console.log(val, 'count被更新');
        },
    },
};
</script>

<template>
    <h1>{{ msg }}</h1>
    <h2>{{ twiceTheCounter }}</h2>
    <p>
        Recommended IDE setup:
        <a href="https://code.visualstudio.com/" target="_blank">VS Code</a>
        +
        <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
    </p>
    <p>See <code>README.md</code> for more information.</p>
    <p>
        <a href="https://vitejs.dev/guide/features.html" target="_blank"> Vite Docs </a>
        |
        <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Docs</a>
    </p>
    <button type="button" @click="count++">count is: {{ count }}</button>
    <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
</template>

<style scoped>
a {
    color: #42b983;
}
label {
    margin: 0 0.5em;
    font-weight: bold;
}

code {
    background-color: #eee;
    padding: 2px 4px;
    border-radius: 4px;
    color: #304455;
}
</style>
