<template>
  <div class="wrapper">
    <div class="difficult">
      <h2>Сложность</h2>
      <input type="radio" value="1500" v-model="timer" />
      <span>Легкий</span>
      <input type="radio" checked value="1000" v-model="timer" />
      <span>Средний</span>
      <input type="radio" value="400" v-model="timer" />
      <span>Сложный</span>

      <button class="start" @click="startGame">Начать</button>
      <h1 v-if="gameOver">ИГРА ОКОНЧЕНА</h1>
    </div>

    <div class="tiles" v-if="gameOn">
      <button
        v-for="(tile, index) in tiles"
        :value="index"
        :key="tile"
        @click="checkRound"
        :class="[{ selected: active == tile }, tile]"
        class="square"
        :style="{ background: tile }"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Simon",
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
      setTimeout(() => {
        this.round();
      }, 500);
    },
    round() {
      this.generateRound();
      this.userRound = [];
      let i = 0;
      setTimeout(() => {
        this.show(i);
      }, 500);
    },
    generateRound() {
      this.gameRound.push(Math.floor(Math.random() * 4));
      this.level++;
    },
    show(i) {
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
      setTimeout(() => {
        this.active = "";
      }, +this.timer);
      if (i < this.level) {
        setTimeout(() => {
          this.show(i);
        }, +this.timer + 300);
      }
    },
    checkRound(event) {
      this.userRound.push(+event.target.value);
      if (
        this.gameRound[this.userRound.length - 1] ==
        this.userRound[this.userRound.length - 1]
      ) {
        if (this.userRound.length == this.level) this.round();
      } else {
        this.gameOver = true;
        this.gameOn = false;
      }
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
  max-width: 500px;
  height: 100%;
  margin: 0 auto;
}
.square {
  width: 40%;
  height: 40%;
  opacity: 0.7;
  border: black 3px solid;
  border-radius: 10px;
  padding-bottom: 40%;
}
.start {
  display: block;
  width: 150px;
  height: 40px;
  font-size: 24px;
  margin: 50px auto;
}
.difficult {
  text-align: center;
}
span {
  margin-right: 15px;
}
.selected,
.square:active {
  opacity: 1;
  border: white 3px solid;
  box-shadow: 0 0 10px red;
}
</style>
