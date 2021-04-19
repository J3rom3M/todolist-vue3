<template>
    <form @submit.prevent="addTechno">
        <label for="techno">Techno à ajouter</label>
        <br>
        <input type="text" name="techno" v-model="techToLearn">
        <br>
        <button type="submit">Ajouter</button>
    </form>
</template>

<script>
import { ref } from '@vue/reactivity';
export default {
    setup(propos, ctx) {
        let techToLearn = ref("");
        const addTechno = function() {
            console.log("Form | addTechno() | techToLearn.value", techToLearn.value);
            ctx.emit("add", techToLearn.value);
            techToLearn.value = "";
        };
        return{
            techToLearn,
            addTechno,
        };
    },
};
</script>

<style>

</style>