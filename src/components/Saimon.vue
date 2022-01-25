<template>
  <div class="wrapper">
    <div class="tiles" v-if="gameOn">
      <button
        v-for="(tile, index) in tiles"
        :value="index"
        :key="tile"
        @click="catchRound"
        :class="[{ selected: active == tile }, tile]"
        class="square"
        :style="{ background: tile }"
      ></button>
    </div>

    <h1 v-if="gameOver">ИГРА ОКОНЧЕНА</h1>
    <button class="start" @click="startGame">Начать</button>
    <div class="difficult">
      <h2>Сложность</h2>
      <input type="radio" value="1500" v-model="timer" />
      <span>Легкий</span>
      <input type="radio" checked value="1000" v-model="timer" />
      <span>Средний</span>
      <input type="radio" value="400" v-model="timer" />
      <span>Сложный</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Saimon",
  data() {
    return {
      tiles: ["red", "blue", "green", "yellow"],
      gameRound: [],
      userRound: [],
      level: 0,
      active: "",
      timer: 1000,
      gameOn: false,
      gameOver: false,
    };
  },
  methods: {
    startGame() {
      this.gameOn = true;
      this.gameOver = false;
      this.active = "";
      this.gameRound = [];
      this.userRound = [];
      this.level = 0;
      this.round();
    },
    round() {
      this.generateRound();
      this.userRound = [];
      let i = 0;
      let around = this;
      this.show(i);
      setTimeout(function () {
        around.active = "";
      }, +around.timer * around.level);
    },
    generateRound() {
      this.gameRound.push(Math.floor(Math.random() * 4));
      this.level++;
    },
    show(i) {
      let around = this;
      this.active = "";
      switch (this.gameRound[i]) {
        case 0:
          this.active = "red";
          break;
        case 1:
          this.active = "blue";
          break;
        case 2:
          this.active = "green";
          break;
        case 3:
          this.active = "yellow";
          break;
      }
      i++;
      setTimeout(function () {
        if (i < around.level) {
          around.show(i);
        }
      }, +around.timer);
    },
    catchRound(event) {
      this.userRound.push(+event.target.value);
      if (this.gameRound.length == this.userRound.length) {
        this.checkRound();
      }
    },
    checkRound() {
      for (let i = 0; i <= this.userRound.length; i++) {
        if (this.gameRound[i] !== this.userRound[i]) {
          this.gameOver = true;
          this.gameOn = false;
        }
      }
      this.round();
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
.wrapper {
  width: 100%;
  height: 100%;
}
.tiles {
  align-content: flex-start;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
  width: 500px;
  height: 500px;
  margin: 0 auto;
}
.square {
  width: 40%;
  height: 40%;
  border: black 3px solid;
  border-radius: 10px;
}
.start {
  display: block;
  width: 150px;
  height: 40px;
  font-size: 24px;
  margin: 0 auto;
}
.difficult {
  text-align: center;
}
span {
  margin-right: 15px;
}
.selected,
.square:active {
  opacity: 0.3;
  border: white 3px solid;
  box-shadow: 0 0 5px red;
}
</style>
