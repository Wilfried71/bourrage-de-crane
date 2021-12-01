<template>
  <div class="container mt-2">
    <h1>Bourrage de crâne anglais</h1>
    <hr>
    <table class="table table-dark">
      <tr>
        <td><b>Mot</b></td>
        <td><b>Traductions</b></td>
      </tr>
      <tr v-for="(d,dkey) of data" :key="dkey">
        <td>{{ d.value }}</td>
        <td>
          <ul>
            <li v-for="(trad, tkey) of d.translations" :key="tkey">{{ trad.value }}</li>
          </ul>
        </td>
      </tr>
    </table>
    <Header></Header>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import data from "./assets/data.js"

export default {
  name: "App",
  components: {
    Header,
  },
  data() {
    return {
      data: data
    }
  }
};
</script>

<style></style>
