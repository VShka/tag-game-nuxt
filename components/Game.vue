<template>
  <div class="game">
    <div class="game__header">
      <div class="game__move-counter">Вы сделали 20 ходов</div>
    </div>
    <div class="game-grid">
      <div
        v-for="(item, index) in arrGridItem"
        :key="index"
        :style="itemsCoordinates[index]"
        ref="div"
        class="game-grid__item"
        @click="moveItem(index)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arrGridItem: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      itemsCoordinates: [],
      emptyItem: {
        top: 0,
        left: 0,
      },
      itemSize: 100,
    }
  },
  created() {
    this.arrGridItem.forEach((item) => {
      const leftPos = item % 4
      const topPos = (item - leftPos) / 4

      const coordinates = {
        top: `${topPos * this.itemSize + 5}px`,
        left: `${leftPos * this.itemSize + 5}px`,
      }

      this.itemsCoordinates.push({
        top: coordinates.top,
        left: coordinates.left,
        element: this.$refs.div,
      })
    })

    this.itemsCoordinates.sort(() => Math.random() - 0.5)
  },
  methods: {
    // itemPos(item) {
    //   const leftPos = item % 4
    //   const topPos = (item - leftPos) / 4

    //   this.itemsCoordinates.push({
    //     top: topPos,
    //     left: leftPos,
    //     element: this.$refs.div,
    //   })

    //   return {
    //     top: `${topPos * this.itemSize + 5}px`,
    //     left: `${leftPos * this.itemSize + 5}px`,
    //     bottom: `${5}px`,
    //     right: `${5}px`,
    //   }
    // },
    moveItem(index) {
      const item = this.itemsCoordinates[index]
      console.log(item)
      // item.top = `${this.emptyItem.top * this.itemSize + 5}px`
      // item.left = `${this.emptyItem.left * this.itemSize + 5}px`
    },
  },
}
</script>

<style lang="scss" scoped>
.game {
  display: flex;
  flex-direction: column;
  align-items: center;

  .game__header {
    display: flex;

    .game__move-counter {
      font-size: 30px;
    }
  }

  .game-grid {
    position: relative;
    width: 400px;
    height: 400px;
    background-color: rgb(202, 229, 219);
    border: 1px solid #000;
    border-radius: 10px;
    padding: 5px;

    .game-grid__item {
      position: absolute;
      display: flex;
      justify-content: center;
      align-items: center;
      color: rgb(201, 112, 29);
      font-size: 60px;
      width: 100px;
      height: 100px;
      border: 1px solid #000;
      border-radius: 10px;
      box-sizing: border-box;
      background-color: rgb(223, 219, 219);
      transition: all 0.3s;
      cursor: pointer;
    }
  }
}
</style>
