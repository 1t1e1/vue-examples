<template>
    <div id="app">
        <p>Calculator</p>
        <MyCalculator />
        <br />
    </div>
</template>

<script>
import MyCalculator from "./components/MyCalculator.vue";

export default {
    name: "app",
    components: {
        MyCalculator,
    },
};
</script>

<style>
#app {
    text-align: center;
    margin: auto;
}
</style>
