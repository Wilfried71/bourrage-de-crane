<template>
  <div class="col-md-12">
    <h2>Score : {{ score }} / {{ nbTrad }}</h2>
    <h3>Correction</h3>
    <table class="table">
      <tr>
        <td><b>Mot</b></td>
        <td><b>Traductions</b></td>
      </tr>
      <tr v-for="(d, dkey) of data" :key="dkey">
        <td>{{ d.value }}</td>
        <td>
          <ul>
            <li v-for="(trad, tkey) of d.translations" :key="tkey">
              <span style="font-weight: bold" class="mr-3">{{ trad.value }}</span>
              <span v-if="trad.found" style="color: rgb(41, 226, 17)">
                Trouvé
              </span>
              <span v-if="!trad.found" style="color: red">Pas trouvé</span>
            </li>
          </ul>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "Correction",
  props: {
    data: [],
    score: Number,
    nbTrad: Number,
  },
};
</script>

<style scoped>
</style>