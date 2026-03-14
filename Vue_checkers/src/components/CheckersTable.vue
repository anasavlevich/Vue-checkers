<template>
  <div class="checkers-table">
    <div class="checkers-table__row" v-for="(row, rowIndex) in table" :key="rowIndex">
      <TableCell class="checkers-table__cell" v-for="(cell, cellIndex) in row"
        :key="rowIndex + '-' + cellIndex + '-' + cell" :data="{ figureType: cell, cx: cellIndex, cy: rowIndex }"
        :class="{ 'checkers-table__cell--highlight': tableHighlight[rowIndex][cellIndex] === 1 }" @showWay="useShowWay"
        @moveChecker="useMoveChecker" />
    </div>
  </div>
</template>

<script setup>
import TableCell from "@/components/TableCell.vue";
import { storeToRefs } from "pinia";
import { useMainStore } from "@/store";
import { useShowWay } from "@/composables/useShowWay";
import { useMoveChecker } from "@/composables/useMoveChecker";

const store = useMainStore();
const { table, tableHighlight } = storeToRefs(store);

</script>

<style lang="less">
.checkers-table {
  display: flex;
  flex-direction: column;
  width: 800px;
  height: 800px;
  margin: 0 auto;
  border: 1px solid @gray;

  &__row {
    display: flex;
    width: 100%;
    background-color: @light_brown;

    &:nth-child(2n) {
      .checkers-table__cell:nth-child(2n + 1) {
        background-color: @brown;
      }
    }

    &:nth-child(2n + 1) {
      .checkers-table__cell:nth-child(2n) {
        background-color: @brown;
      }
    }
  }

  &__cell {
    position: relative;

    &--highlight {
      &::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: @green;
        opacity: 0.5;
      }
    }
  }
}
</style>