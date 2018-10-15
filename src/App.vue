<template>
  <div id="app">
    <div class="container">
      <p>Najviac koľko rôznych domčekov vieš vytvoriť tak, že ani jeden nebude vyfarbený rovnako ako ostatné?</p>
      <div class="row">
        <div class="col-10">
          <el-input placeholder="Please input" v-model="input"></el-input>
        </div>
        <div class="col-2">
          <el-button @click="checkAnswer">Check</el-button>
        </div>
      </div>
      <div class="row">
        <div class="col-10">
      <div class="row">
        <div class="col-2" v-for="n in houseCount">
          <house :selectedColor="color"></house>
        </div>
        <div class="col-2">
          <el-button @click="addHouse">Add</el-button>
        </div>
      </div>
    </div>
        <div class="col-1">
          <swatches v-model="color" :colors="colors" inline></swatches>
        </div>
    </div>
    </div>
    </div>
</template>

<script>
    import House from "./components/House";
    import Swatches from "vue-swatches"

    export default {
        name: 'app',
        data() {
            return {
                input: 1,
                houseCount: 1,
                color: '#000',
                colors: ['#000000', '#FFEEAA', '#F891A6']
            }
        },
        components: {
            House,
            Swatches
        },
        methods: {
          addHouse() {
              this.houseCount++;
              this.input = this.houseCount;
          },
          checkAnswer() {
              if (Math.pow(this.colors.length, 2) == this.input) {
                  alert("ok");
              }
              else {
                  alert("wrong")
              }
          }
        }
    }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
