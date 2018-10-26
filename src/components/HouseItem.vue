<template>
  <div class="house">
    <div @click="changeSquareColor" class="house-square" :style="backgroundSquare"></div>
    <div @click="changeRoofColor" class="house-roof" :style="backgroundRoof"></div>
  </div>
</template>

<script>
    export default {
        name: "HouseItem",
        props: ['selectedColor'],
        data() {
            return {
                changed: true,
                backgroundRoof: {
                    backgroundColor: "white"
                },
                backgroundSquare: {
                    backgroundColor: "white"
                }
            }
        },
        methods: {
            changeRoofColor() {
                this.backgroundRoof.backgroundColor = this.selectedColor;
                this.changeItemProperty()
            },
            changeSquareColor() {
                this.backgroundSquare.backgroundColor = this.selectedColor;
                this.changeItemProperty()
            },
            changeItemProperty() {
                if(this.backgroundRoof.backgroundColor === "white" && this.backgroundSquare.backgroundColor === "white") {
                    this.$emit("whiteItem")
                }
                else {
                    this.$emit("colorItem")
                }
            }
        }
    }
</script>

<style scoped lang="scss">
  .house {
    position: relative;
    &-square {
      border: 2px solid #000;
      height: 100px;
      width: 100px;
      position: relative;
      margin-top: 100px;
      z-index: 1;
    }
    &-roof {
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
</style>