<template>
  <div class="flag">
    <div @click="changeFirstColor" class="flag-item first" :style="backgroundFirst"></div>
    <div @click="changeSecondColor" class="flag-item second" :style="backgroundSecond"></div>
    <div @click="changeThirdColor" class="flag-item third" :style="backgroundThird"></div>
  </div>
</template>

<script>
    export default {
        name: "FlagItem",
        props: ['selectedColor'],
        data() {
            return {
                changed: true,
                backgroundFirst: {
                    backgroundColor: "white"
                },
                backgroundSecond: {
                    backgroundColor: "white"
                },
                backgroundThird: {
                    backgroundColor: "white"
                }
            }
        },
        methods: {
            changeFirstColor() {
                this.backgroundFirst.backgroundColor = this.selectedColor;
                this.changeItemProperty()
            },
            changeSecondColor() {
                this.backgroundSecond.backgroundColor = this.selectedColor;
                this.changeItemProperty()
            },
            changeThirdColor() {
                this.backgroundThird.backgroundColor = this.selectedColor;
                this.changeItemProperty()
            },
            changeItemProperty() {
                this.$emit("colorsArray", ["asf", "sdfdas"]);
                if(this.backgroundFirst.backgroundColor === "white" && this.backgroundSecond.backgroundColor === "white" && this.backgroundThird.backgroundColor === "white") {
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
.flag {
  position: relative;
  height: 99px;

  &-item {
    width: 100%;
    height: 33%;
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