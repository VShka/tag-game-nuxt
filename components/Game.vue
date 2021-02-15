<template>
  <div class="game">
    <div class="game__header">
      <div class="game__move-counter">Кол-во шагов:{{ stepCounter }}</div>
    </div>
    <div class="game-grid" :style="gridArea">
      <div
        v-for="(item, index) in arrGridItem"
        :key="index"
        :style="itemsCoordinates[index]"
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
      itemsCoordinates: [
        { 'grid-area': 'one' },
        { 'grid-area': 'two' },
        { 'grid-area': 'three' },
        { 'grid-area': 'four' },
        { 'grid-area': 'five' },
        { 'grid-area': 'six' },
        { 'grid-area': 'seven' },
        { 'grid-area': 'eight' },
        { 'grid-area': 'nine' },
        { 'grid-area': 'ten' },
        { 'grid-area': 'eleven' },
        { 'grid-area': 'twelve' },
        { 'grid-area': 'thirteen' },
        { 'grid-area': 'fourteen' },
        { 'grid-area': 'fifteen' },
        { 'grid-area': 'empty' },
      ],
      emptyItem: { 'grid-area': 'empty' },
      itemSize: 100,
      stepCounter: 0,
      gridArea: {
        'grid-template-areas': `'one two three four'
                                'five six seven eight'
                                'nine ten eleven twelve'
                            'thirteen fourteen fifteen empty'`,
      },
    }
  },
  created() {
    this.arrGridItem.sort(() => Math.random() - 0.5)
  },
  methods: {
    moveItem(index) {
      const item = this.itemsCoordinates[index]
      const emptyItem = this.emptyItem['grid-area']
      const itemGrid = item['grid-area']

      item['grid-area'] = emptyItem
      this.emptyItem['grid-area'] = itemGrid

      this.stepCounter++
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
    display: grid;
    width: 400px;
    height: 400px;
    background-color: rgb(202, 229, 219);
    border: 1px solid #000;
    border-radius: 10px;
    padding: 5px;

    .game-grid__item {
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
      transition: all linear 0.3s;
      cursor: pointer;
    }
  }
}
</style>
