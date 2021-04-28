<template>
  <div class="container">
    <h1>Fast Click</h1>
    <div>
      <p>Objectif, faire le plus clics en 10s</p>
      <h2 v-if="gameStatus == 1">Vous avez fait {{ totalClick }} clics</h2>
      <p v-if="gameStatus == 1">{{ totalErrorClick }} erreur(s)</p>
      <h2 v-if="gameStatus == 2">{{ finishTime }}s</h2>
      <p v-if="gameStatus != 2" style="cursor:pointer; margin-bottom: 20px; border: 1px solid #252525; margin-top: 10px" @click="startGame">Lancer le jeu</p>
    </div>
    <div class="game">
      <div :style="actual == 1 ? 'background: blue' : ''" @click="nextCase(1)" class="clicker"></div>
      <div :style="actual == 2 ? 'background: red' : ''" @click="nextCase(2)" class="clicker"></div>
      <div :style="actual == 3 ? 'background: green' : ''" @click="nextCase(3)" class="clicker"></div>
      <div :style="actual == 4 ? 'background: yellow' : ''" @click="nextCase(4)" class="clicker"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      actual: 0,
      finishTime: 0,
      totalClick: 0,
      totalErrorClick: 0,

      gameStatus: 0,
    }
  },
  methods: {
    startGame() {
      this.finishTime = 11;
      this.gameStatus = 2
      this.totalClick = 0;
      this.totalErrorClick = 0;
      var x = parseInt((Math.random () * 4) + 1)
      this.countDown()
      this.actual = x;
    },
    countDown: function() {
      this.finishTime -= 1
      if (this.finishTime > 0) {
        setTimeout(this.countDown,1000);
      } else {
        console.log('Finish')
        this.actual = 0
        this.gameStatus = 1
      }
    },
    nextCase(id) {
      if (id == this.actual && this.finishTime != 0) {
        this.totalClick += 1
        var x = parseInt((Math.random () * 4) + 1)
        while (x == this.actual) {
          x = parseInt((Math.random () * 4) + 1)
        }
        this.actual = x;
      } else if (id != this.actual && this.finishTime != 0) {
        this.totalErrorClick += 1
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.game {
  display: flex;
}
.clicker {
  cursor: pointer;
  padding: 60px;
}
h1 {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
