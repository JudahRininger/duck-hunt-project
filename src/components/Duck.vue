<template>
  <div class="duck" :style="{top: top + '%', left: left + '%'}">
      <img src="../assets/flap.png" alt="" @click="addPoints" v-show="clickable">
      <img src="../assets/shot-duck.png" alt="" v-show="!clickable">
  </div>
</template>

<script>

export default {
    name: "Duck",
    props: {
    },
    data() {
        return {
            top: 4,
            left: 40,
            clickable: true

        };
    },
    methods: {
        addPoints() {
            if(this.clickable) {
                this.$emit("addPoints")
            }
            this.clickable = false;
        },
        reset() {
            this.$emit("reset")
        },
        move() {
            if(this.clickable){
                this.left +=1
                setTimeout(() => this.move(), 100);
            }
        }

    },
    mounted () {
        this.top = Math.random()* 100 - 25;
        this.left = Math.random()*85 + 5;
        this.clickable = true;
        setTimeout(() => this.reset(), 1500);
        this.move();
    }

}
</script>

<style scoped>
.duck {
    position: absolute;
    transition: ease;
    width: 80px;
    left: 75%;
    top: 50%;
}
img {
    width: 100%;
}

</style>