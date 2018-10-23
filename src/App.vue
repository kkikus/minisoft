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
            <div class="col-6 col-sm-4 col-md-2" v-for="n in houseCount">
              <flag-item :selectedColor="color"></flag-item>
            </div>
            <div class="col-6 col-sm-4 col-md-2">
              <div @click="addHouse" class="flag-button button">

                <div class="flag-button-item first"></div>
                <div class="flag-button-item second"></div>
                <div class="flag-button-item third"></div>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50" width="30" height="30" class="house-button-icon">
                  <path d="M 25 2 C 12.309295 2 2 12.309295 2 25 C 2 37.690705 12.309295 48 25 48 C 37.690705 48 48 37.690705 48 25 C 48 12.309295 37.690705 2 25 2 z M 25 4 C 36.609824 4 46 13.390176 46 25 C 46 36.609824 36.609824 46 25 46 C 13.390176 46 4 36.609824 4 25 C 4 13.390176 13.390176 4 25 4 z M 24 13 L 24 24 L 13 24 L 13 26 L 24 26 L 24 37 L 26 37 L 26 26 L 37 26 L 37 24 L 26 24 L 26 13 L 24 13 z"/>
                </svg>
              </div>
              <!--<div @click="addHouse" class="circle-button button">
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50" width="30" height="30" class="house-button-icon">
                    <path d="M 25 2 C 12.309295 2 2 12.309295 2 25 C 2 37.690705 12.309295 48 25 48 C 37.690705 48 48 37.690705 48 25 C 48 12.309295 37.690705 2 25 2 z M 25 4 C 36.609824 4 46 13.390176 46 25 C 46 36.609824 36.609824 46 25 46 C 13.390176 46 4 36.609824 4 25 C 4 13.390176 13.390176 4 25 4 z M 24 13 L 24 24 L 13 24 L 13 26 L 24 26 L 24 37 L 26 37 L 26 26 L 37 26 L 37 24 L 26 24 L 26 13 L 24 13 z"/>
                  </svg>
              </div>-->
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
    import CircleItem from "./components/CircleItem";
    import FlagItem from "./components/FlagItem";
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
            FlagItem,
            CircleItem,
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

  .button {
    cursor: pointer;
    position: relative;
  }

  .house-button {
    &:hover {
      .house-button-roof, .house-button-square {
        background: #777;
      }
    }
    &-icon {
      position: absolute;
      background-color: #FFF;
      border-radius: 50%;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    &-square {
      background: #AAA;
      border: 2px solid #000;
      height: 100px;
      width: 100px;
      position: relative;
      margin-top: 100px;
      z-index: 1;
    }
    &-roof {
      background: #AAA;
      position: absolute;
      top: -20px;
      left: -20px;
      border-left: 2px solid #000;
      border-top: 2px solid #000;
      height: 70px;
      overflow: hidden;
      width: 70px;
      transform: rotate(45deg);
      transform-origin: 100% 100%;
      z-index: 0;
    }
  }

  .circle-button {
    background: #AAA;
    border-radius: 50%;
    border: 2px solid black;
    height: 100px;
    width: 100px;
    &:hover {
      background: #777;
    }
    &-icon {
      position: absolute;
      background-color: #FFF;
      border-radius: 50%;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }

  .flag-button {
    height: 99px;
    &:hover {
      .flag-button-item {
        background: #777;
      }
    }
    &-icon {
      position: absolute;
      background-color: #FFF;
      border-radius: 50%;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    &-item {
      width: 100%;
      height: 33%;
      background-color: #AAA;
      border: 1px solid black;
      position: absolute;
      &.first {
        top: 0;
        border-bottom: 0;
      }
      &.second {
        top: 33%;
        border-bottom: 0;
      }
      &.third {
        top: 66%;
      }
    }
  }

</style>
