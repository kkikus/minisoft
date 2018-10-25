<template>
  <div id="app">
    <div class="container">
      <p>{{itemSettings[currentLevel.itemType].question}} Použi všetky farby na palete vpravo.</p>
      <div class="row">
        <div class="col-10">
          <el-input placeholder="Please input" v-model="currentLevel.input"></el-input>
        </div>
        <div class="col-2">
          <el-button @click="checkAnswer">Skontroluj</el-button>
        </div>
      </div>
      <div class="row">
        <div class="col-10">
          <div class="row">
            <div class="col-6 col-sm-4 col-md-2 mb-4" v-for="(item, index) in items" @click.middle="deleteItem(index)">
              <flag-item v-show="currentLevel.itemType=='flag'" :selectedColor="color"></flag-item>
              <circle-item v-show="currentLevel.itemType=='circle'" :selectedColor="color"></circle-item>
              <house v-show="currentLevel.itemType=='house'" :selectedColor="color"></house>
            </div>
            <div class="col-6 col-sm-4 col-md-2">
              <div v-show="currentLevel.itemType=='flag'" @click="addItem" class="flag-button button">
                <div class="flag-button-item first"></div>
                <div class="flag-button-item second"></div>
                <div class="flag-button-item third"></div>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50" width="30" height="30" class="house-button-icon">
                  <path d="M 25 2 C 12.309295 2 2 12.309295 2 25 C 2 37.690705 12.309295 48 25 48 C 37.690705 48 48 37.690705 48 25 C 48 12.309295 37.690705 2 25 2 z M 25 4 C 36.609824 4 46 13.390176 46 25 C 46 36.609824 36.609824 46 25 46 C 13.390176 46 4 36.609824 4 25 C 4 13.390176 13.390176 4 25 4 z M 24 13 L 24 24 L 13 24 L 13 26 L 24 26 L 24 37 L 26 37 L 26 26 L 37 26 L 37 24 L 26 24 L 26 13 L 24 13 z"/>
                </svg>
              </div>
              <div v-show="currentLevel.itemType=='circle'" @click="addItem" class="circle-button button">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50" width="30" height="30" class="house-button-icon">
                  <path d="M 25 2 C 12.309295 2 2 12.309295 2 25 C 2 37.690705 12.309295 48 25 48 C 37.690705 48 48 37.690705 48 25 C 48 12.309295 37.690705 2 25 2 z M 25 4 C 36.609824 4 46 13.390176 46 25 C 46 36.609824 36.609824 46 25 46 C 13.390176 46 4 36.609824 4 25 C 4 13.390176 13.390176 4 25 4 z M 24 13 L 24 24 L 13 24 L 13 26 L 24 26 L 24 37 L 26 37 L 26 26 L 37 26 L 37 24 L 26 24 L 26 13 L 24 13 z"/>
                </svg>
              </div>
              <div v-show="currentLevel.itemType=='house'" @click="addItem" class="house-button button">
                <div class="house-button-square">
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50" width="30" height="30" class="house-button-icon">
                    <path d="M 25 2 C 12.309295 2 2 12.309295 2 25 C 2 37.690705 12.309295 48 25 48 C 37.690705 48 48 37.690705 48 25 C 48 12.309295 37.690705 2 25 2 z M 25 4 C 36.609824 4 46 13.390176 46 25 C 46 36.609824 36.609824 46 25 46 C 13.390176 46 4 36.609824 4 25 C 4 13.390176 13.390176 4 25 4 z M 24 13 L 24 24 L 13 24 L 13 26 L 24 26 L 24 37 L 26 37 L 26 26 L 37 26 L 37 24 L 26 24 L 26 13 L 24 13 z"/>
                  </svg>
                </div>
                <div class="house-button-roof"></div>
              </div>

            </div>
          </div>
        </div>
        <div class="col-1">
          <swatches v-model="color" :colors="currentLevel.gameColors" inline></swatches>
          <svg @click="color='#FFF'" xmlns="http://www.w3.org/2000/svg" class="rubber-icon" width="64" height="64" viewBox="0 0 16 16">
            <path fill="#444444" d="M8.1 14l6.4-7.2c0.6-0.7 0.6-1.8-0.1-2.5l-2.7-2.7c-0.3-0.4-0.8-0.6-1.3-0.6h-1.8c-0.5 0-1 0.2-1.4 0.6l-6.7 7.6c-0.6 0.7-0.6 1.9 0.1 2.5l2.7 2.7c0.3 0.4 0.8 0.6 1.3 0.6h11.4v-1h-7.9zM6.8 13.9c0 0 0-0.1 0 0l-2.7-2.7c-0.4-0.4-0.4-0.9 0-1.3l3.4-3.9h-1l-3 3.3c-0.6 0.7-0.6 1.7 0.1 2.4l2.3 2.3h-1.3c-0.2 0-0.4-0.1-0.6-0.2l-2.8-2.8c-0.3-0.3-0.3-0.8 0-1.1l3.5-3.9h1.8l3.5-4h1l-3.5 4 3.1 3.7-3.5 4c-0.1 0.1-0.2 0.1-0.3 0.2z"/>
          </svg>
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
                currentLevel: {
                    id: 0,
                    colorsNumber: 1,
                    gameColors: [],
                    input: 1,
                    itemType: "circle",
                    isRepeated: Math.random() > .5,
                },
                items: [
                    {id: 1, isColoured: false}
                ],
                color: '',
                colors: ['#FF6633', '#FF33FF', '#FFFF99', '#00B3E6', '#E6B333', '#3366E6', '#999966', '#99FF99', '#B34D4D', '#6680B3', '#66991A', '#FF99E6', '#CCFF1A', '#E6331A', '#33FFCC', '#B366CC', '#4D8000', '#B33300', '#66664D', '#991AFF', '#33991A', '#B3B31A', '#809980', '#999933', '#66E64D', '#E64D66', '#4DB380', '#6666FF'],
                levels: [
                    {
                        itemType: "circle",
                        minColors: 1,
                        maxColors: 2,
                    }, {
                        itemType: "circle",
                        minColors: 3,
                        maxColors: 4,
                    }, {
                        itemType: "circle",
                        minColors: 4,
                        maxColors: 6,
                    }, {
                        itemType: "house",
                        minColors: 2,
                        maxColors: 2,
                    }, {
                        itemType: "house",
                        minColors: 3,
                        maxColors: 3,
                    }, {
                        itemType: "flag",
                        minColors: 2,
                        maxColors: 2,
                    }, {
                        itemType: "flag",
                        minColors: 3,
                        maxColors: 3,
                    }, {
                        itemType: "house",
                        minColors: 4,
                        maxColors: 5,
                    }
                ],
                itemSettings: {
                    "circle": {
                        parts: 1,
                        question: "Najviac koľko rôznych kruhov vieš vytvoriť tak, že ani jeden nebude vyfarbený rovnako ako ostatné?"
                    },
                    "house": {
                        parts: 2,
                        question: "Najviac koľko rôznych domčekov vieš vytvoriť tak, že ani jeden nebude vyfarbený rovnako ako ostatné?"
                    },
                    "flag": {
                        parts: 3,
                        question: "Najviac koľko rôznych vlajok vieš vytvoriť tak, že ani jedna nebude vyfarbená rovnako ako ostatné?"
                    }
                }
            }
        },
        components: {
            FlagItem,
            CircleItem,
            House,
            Swatches
        },
        created() {
            let currentLevel = this.currentLevel.id;
            this.generateColors(currentLevel);
            this.currentLevel.itemType = this.levels[currentLevel].itemType
        },
        methods: {
            addItem() {
                this.items.push({
                    id: this.items.length + 1,
                    isColoured: false
                })
            },
            checkAnswer() {
                if (Math.pow(this.currentLevel.colorsNumber, this.itemSettings[this.currentLevel.itemType].parts) == this.currentLevel.input) {
                    if (this.currentLevel.id < this.levels.length - 1) {
                        this.$confirm("Výborne, vaša odpoveď bola správna!", "Správne!", {
                            confirmButtonText: 'Ďalší level',
                            cancelButtonText: 'Znovu',
                            type: "success"
                        }).then(() => {
                            this.resetValues();
                            if (this.currentLevel.isRepeated) {
                                this.repeatLevel();
                            }
                            else {
                                this.nextLevel()
                            }
                        }).catch(() => {
                            this.resetValues();
                            this.repeatLevel();
                        })
                    }
                    else {
                        this.finish()
                    }
                }
                else {
                    this.$message.error('Nesprávna odpoveď!');
                }
            },
            deleteItem(id) {
                this.items.splice(id, 1)
            },
            finish() {
                this.$alert("Vyriešili ste všetky úlohy, gratulujeme!", "Gratulujeme!", {
                    confirmButtonText: 'Nová hra',
                    type: "success",
                    callback: action => {
                        this.resetValues();
                        this.currentLevel.id = 0;
                        this.currentLevel.itemType = 'circle';
                        this.currentLevel.isRepeated = Math.random() > .5;
                        this.generateColors(this.currentLevel.id)
                    }
                })
            },
            generateColors(currentLevel) {
                let min = this.levels[currentLevel].minColors;
                let max = this.levels[currentLevel].maxColors;
                this.currentLevel.colorsNumber = Math.floor(Math.random() * (max - min + 1)) + min;
                let shuffled = this.colors.sort(() => {
                    return .5 - Math.random()
                });
                this.currentLevel.gameColors = shuffled.slice(0, this.currentLevel.colorsNumber);
            },
            nextLevel() {
                this.currentLevel.id++;
                this.generateColors(this.currentLevel.id)
                this.currentLevel.itemType = this.levels[this.currentLevel.id].itemType;
                this.currentLevel.isRepeated = Math.random() < .5;
            },
            repeatLevel() {
                this.currentLevel.isRepeated = false;
                this.generateColors(this.currentLevel.id)
            },
            resetValues() {
                this.items = [
                    {id: 1, isColoured: false}
                ];
                this.color = '';
                this.currentLevel.input = 1;
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

  .rubber-icon {
    cursor: pointer;
    &:hover {
      path {
        fill: red;
      }
    }
  }
</style>
