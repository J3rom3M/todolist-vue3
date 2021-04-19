<template>
  <img alt="Vue logo" src="./assets/todolist.jpg">
  <h1>Veille technologique</h1>
  <Form @add="saveTechno" />
  <br />
  <TechnoList :technos="technos" @delete-techno="deleteTechno" @edit-techno="editTechno" />
</template>

<script>
import Form from '@/components/Form';
import TechnoList from '@/components/TechnoList';
import { ref } from '@vue/reactivity';

export default {
  name: 'App',
  components: {
    Form,
    TechnoList,
  },
  setup() {
    let technos = ref([]);

    const saveTechno = function (data) {
      console.log("App | saveTechno() | data", data);
      technos.value = [...technos.value, { techno: data, id: Date.now() }];
      console.log("App | saveTechno() | technos.value", data);
    };
    const editTechno = function (tech) {
      technos.value = technos.value.map(t => t.id !== tech.id ? t : tech);
    }

    const deleteTechno = function (tech) {
      console.log("App | deleteTechno() | tech", tech);
      technos.value = technos.value.filter(t => t.id !== tech.id);
    }

    return {
      saveTechno,
      editTechno,
      deleteTechno,
      technos
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
