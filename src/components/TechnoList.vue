<template>
    <h3>Toutes les technos à veiller</h3>
    {{technos.length}} techno{{technos.length > 1 ? 's' : ''}}
    <ul>
        <li v-for="tech in technos" :key="tech.id">
            <button @click="editTechno(tech)">T</button>
            <button @click="deleteTechno(tech)">X</button>
            <span v-if="technoToEdit !== null && technoToEdit.id === tech.id">
                <input type="text" v-model="technoToEdit.techno" @keypress.enter="save" />
                <button @click="save">OK</button>
            </span>
            <span v-else>
                {{tech.techno}}
            </span>
            
        </li>
    </ul>
</template>

<script>
import { ref } from '@vue/reactivity';
export default {
    emits: ["delete-techno", "edit-techno"],
    props: {
        technos: {
            type: Array,
            required: true
        },
    },
    setup(props, {emit}) {
        let technoToEdit = ref(null);

        let deleteTechno = function(tech) {
            emit('delete-techno', tech);
        };
        let editTechno = function(tech) {
            technoToEdit.value = tech;
        };
        let save = function () {
            emit('edit-techno', technoToEdit.value);
            technoToEdit.value = null;
        };

        return {
            deleteTechno,
            editTechno,
            save,
            technoToEdit,
        };
    },
};
</script>

<style>

    ul {
    list-style: none;
    width: 50%;
    margin-left: 40%;
    text-align: left;
    }
</style>