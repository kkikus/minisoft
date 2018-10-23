<template>
  <div @click="changeFillColor" class="circle" :style="background"></div>
</template>

<script>
    export default {
        name: "CircleItem",
        props: ['selectedColor'],
        data() {
            return {
                changed: true,
                background: {
                    backgroundColor: "white"
                }
            }
        },
        methods: {
            changeFillColor() {
                this.background.backgroundColor = this.selectedColor
            }
        }
    }
</script>

<style scoped lang="scss">
  .circle {
    border: 2px solid black;
    border-radius: 50%;
    height: 100px;
    width: 100px;
  }
</style>