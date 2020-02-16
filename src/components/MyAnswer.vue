<template>
    <div>
        Ask a yes/no question:
        <input type="text" v-model="question" />
        <p>a:{{ answer }}</p>
        <br />
        <MyAxios />
    </div>
</template>

<script>
import axios from "axios";
import _ from "lodash";
import MyAxios from "./MyAxios.vue";

export default {
    name: "myanswer",
    components: {
        MyAxios,
    },
    data: function() {
        return {
            question: "",
            answer: "I cannot give you an answer until you ask a question!",
        };
    },
    methods: {
        isQuestionValid: function() {
            this.sendRequest();
        },
        sendRequest: _.debounce(function() {
            if (this.question.indexOf("?") == -1) {
                this.answer = "Questions usually contain a question mark. ;-)";
                return;
            }
            axios
                .get("https://yesno.wtf/api")
                .then(response => {
                    console.log(this);
                    this.answer = response.data.answer;
                })
                .catch(error => console.log(error));
        }, 1000),
    },
    watch: {
        question: function() {
            this.answer = "Waiting for you to stop typing...";
            this.sendRequest();
        },
    },
};
</script>

<style></style>
