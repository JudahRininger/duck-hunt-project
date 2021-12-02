<template>
  <div class="top">
    <div class="row">
      <table>
        <tr>
          <h2>Total: {{total}}</h2>
          <h2>Time Remaining: {{timeRemaining}}</h2>
        </tr>
      </table>
      <h2 class="down">High Score: {{highScore}}</h2>
    </div>
  </div>
  <div class="space"></div>

  <div class="background">
    <div class="sky">
    <Duck v-if="isPlaying" @addPoints="addPoints" @reset="reset" />
    <Duck v-if="isPlaying" @addPoints="addPoints"/>
    <Duck v-if="isPlaying" @addPoints="addPoints"/>
    </div>
    
    <div class="ground row">
      <button class="btn" @click="startGame"> Start </button>
      <button class="btn" @click="fullStop"> Stop </button>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Duck from './components/Duck.vue'

export default {
  name: 'App',
  components: {
    Duck
  },
  data() {
    return{
      highScore: 0,
      total: 0,
      timeRemaining: 0,
      isPlaying: false,
    }
  },
  methods: {
    async startGame() {
      if(this.isPlaying) {
        this.timeRemaining = 20;
        this.total = 0;
      }
      else {
      this.isPlaying = true;
      this.timeRemaining = 20;
      this.total = 0;
      this.setTimer()
      }
    },
    stopGame() {
      this.isPlaying = false;
    },
    fullStop() {
      this.isPlaying = false;
      this.timeRemaining = 0;
    },
    addPoints() {
      this.total++;
    },
    reset() {
      this.isPlaying = false;
      if (this.timeRemaining > 0) {
        setTimeout(() => this.isPlaying = true, 100);
      }
    },
    setTimer() {
      if(this.timeRemaining > 0) {
        setTimeout(() => this.timeRemaining--, 1000);
        setTimeout(() => this.setTimer(), 1000);
      }
      else {
        this.stopGame();
        if (this.total > this.highScore) {
          this.highScore = this.total;
        }
      }
      if(this.timeRemaining < 0) {
          this.timeRemaining = 0;
        }

    }


  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.top {
  height: 12vh;
  padding: 2vh;
  background-color: rgb(129, 191, 230);
}
.sky {
  height: 56vh;
  position: relative;
  border: none;
}
.background {
  background-image: url("./assets/background.png");
  background-color: lightskyblue;
  border: none;
  height: 70vh;
}
.space {
  padding-top: 18vh;
  background-color: lightskyblue;
  border: none;
}
.ground {
}
.row {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.btn {
  width: 10vh;
  height: 10vh;
  justify-content: center;
  margin-top: 3vh;
  border-radius: 50%;
}
.down {
  padding-top: 2vh;
}
</style>
