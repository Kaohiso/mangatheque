<template>
  <div class="bookshelf">
    <div v-for="(slot, index) in slots" :key="index" class="slot" :style="getStyle(slot)">
      <div v-for="index in 7 * slot.colSpan">
        <div class="book"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Bookshelf',
  data() {
    return {
      slots: [
        { label: '1', colStart: 1, colSpan: 1, rowSpan: 2 },
        { label: '2', colStart: 2, colSpan: 1, rowSpan: 2 },
        { label: '3', colStart: 3, colSpan: 1, rowSpan: 2 },
        { label: '4', colStart: 4, colSpan: 1, rowSpan: 2 },
        { label: '5', colStart: 1, colSpan: 1, rowSpan: 2 },
        { label: '6', colStart: 2, colSpan: 2, rowSpan: 2 },
        { label: '7', colStart: 4, colSpan: 1, rowSpan: 2 },
        { label: '8', colStart: 1, colSpan: 1, rowSpan: 2 },
        { label: '9', colStart: 2, colSpan: 1, rowSpan: 2 },
        { label: '10', colStart: 3, colSpan: 1, rowSpan: 2 },
        { label: '11', colStart: 4, colSpan: 1, rowSpan: 2 },
        { label: '12', colStart: 1, colSpan: 1, rowSpan: 2 },
        { label: '13', colStart: 2, colSpan: 1, rowSpan: 2 },
        { label: '14', colStart: 3, colSpan: 2, rowSpan: 2 },
        { label: '15', colStart: 1, colSpan: 1, rowSpan: 2 },
        { label: '16', colStart: 2, colSpan: 1, rowSpan: 2 },
        { label: '17', colStart: 3, colSpan: 1, rowSpan: 2 },
        { label: '18', colStart: 4, colSpan: 1, rowSpan: 2 },
      ],
    }
  },
  methods: {
    getStyle(slot) {
      return {
        gridColumn: `${slot.colStart} / span ${slot.colSpan}`,
        gridRow: `span ${slot.rowSpan}`,
      }
    },
  },
}
</script>

<style scoped>
.bookshelf {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 50px;
  gap: 10px;
  width: 900px;
  margin: auto;
  padding: 10px;
  background: #f0ece7;
  border-radius: 5px;
  background-color: #7b3f00;
}

.slot {
  background: #d9c2a3;
  border-radius: 3px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  color: #7b3f00;
  gap: 4px;
}

.book {
  border: solid 1px;
  height: 100px;
  width: 26px;
}
</style>
