<template>
  <div class="container mt-2">
    <Header msg="Bourrage de crâne anglais"></Header>
    <!-- <button class="btn btn-danger mb-2" @click="startGame()" v-if="gameState == 1">Reset</button> -->
    <div class="col-md-12" v-if="gameState == 0">
      <!-- Start button -->
      <div class="d-flex justify-content-center">
        <button class="btn btn-primary mb-2" @click="startGame()">
          Commencer le test
        </button>
      </div>
    </div>    
    <div class="col-md-12" v-if="gameState == 0">      
      <!-- Table -->
      <table class="table table-dark">
        <tr>
          <td><b>Mot</b></td>
          <td><b>Traductions</b></td>
        </tr>
        <tr v-for="(d, dkey) of data" :key="dkey">
          <td>{{ d.value }}</td>
          <td>
            <ul>
              <li v-for="(trad, tkey) of d.translations" :key="tkey">
                {{ trad.value }}
              </li>
            </ul>
          </td>
        </tr>
      </table>
    </div>
    <Game
      v-if="gameState == 1"
      :data="currentGameList"
      :currentIndex="currentIndex"
      @nextItem="nextItem"
    ></Game>
    <Correction
      v-if="gameState == 2"
      :data="currentGameList"
      :score="score"
      :nbTrad="nbTrad"
    ></Correction>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Game from "./components/Game.vue";
import Correction from "./components/Correction.vue";
import data from "./assets/data.js";

export default {
  name: "App",
  components: {
    Header,
    Game,
    Correction,
  },
  data() {
    return {
      data: data,
      gameState: 0,
      currentIndex: 0,
      currentGameList: [],
      nbTrad: 0,
      score: 0,
      startGame: () => {
        this.gameState = 1;
        this.currentGameList = this.shuffleList(data);
      },
      shuffleList: (arr) => {
        let newArr = arr.sort(() => 0.5 - Math.random());
        newArr.forEach((item) => {
          item.translations.forEach((t) => {
            t.found = false;
          });
        });
        return newArr;
      },
      matchResponses(responses) {
        this.currentGameList[this.currentIndex].translations.forEach((item) => {
          // console.log(item, responses);
          if (
            Object.values(responses).filter(
              (r) => r.toUpperCase() == item.value.toUpperCase()
            ).length > 0
          ) {
            item.found = true;
          }
        });
      },
      calculScore() {
        this.nbTrad = 0;
        this.score = 0;
        for (let i = 0; i < this.currentGameList.length; i++) {
          for (
            let j = 0;
            j < this.currentGameList[i].translations.length;
            j++
          ) {
            this.nbTrad++;
            if (this.currentGameList[i].translations[j].found == true) {
              this.score++;
            }
          }
        }
      },
    };
  },
  methods: {
    // When pass to another item
    nextItem(event) {
      //console.log(event);
      this.matchResponses(event);
      event = [];
      this.currentIndex++;
      // If end of game
      if (this.currentIndex == this.currentGameList.length) {
        this.calculScore();
        this.gameState = 2;
      }
    },
  },
};
</script>

<style></style>
