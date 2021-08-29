<template>
    <form class="Imperial-units" action="">
        <input v-if="showElement" v-model="username.userInput" class="agent-name" type="text" name="name" placeholder="Type Your Name">
        <Head :unites="unites" :type="type" />
        <Body :result="result" :unites="unites" :conclusion="conclusion" :personData="personData" :showElement="showElement" />
        <Buttons @claculate="claculate" @saveData="saveData" :showElement="showElement" />
    </form>
</template>

<script>
import Head from './Head.vue'
import Body from './Body.vue' 
import Buttons from './Buttons.vue'
export default {
    props: ["showElement", "personData", "result", "conclusion", "type", "unites", "username"],
    components: {
        Head,
        Body,
        Buttons
    },
    methods: {
        claculate() {
            this.$emit("claculate")
        },
        saveData() {
            this.$emit("saveData")
        }
    }
}
</script>

<style>
input {
    outline: none; 
}
.Imperial-units {
    padding: 10px;
}

.agent-name {
    width: 100%;
    border: none;
    border-radius: 4px;
    -webkit-border-radius: 4px;
    -moz-border-radius: 4px;
    -ms-border-radius: 4px;
    -o-border-radius: 4px;
    padding: 6px 0;
    margin-top: 15px;
    text-align: center;
}

.agent-name::placeholder {
    text-align: center;
    color: #581845;
}

</style>