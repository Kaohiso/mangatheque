<template>
  <!-- <div
    class="book"
    :draggable="true"
    style="background-color: red; cursor: pointer; height: 100px; width: 26px; margin-bottom: 20px"
    @dragstart="onDragStart"
  ></div> -->

  <div class="bookshelf wood-texture">
    <div v-for="(slot, index) in cases" :key="index" class="case" :style="getStyle(slot)">
      <div v-for="(_, slotIndex) in Array(7 * slot.colSpan)" :key="slotIndex">
        <div
          class="slot"
          :data-shelf-position="`${index}-${slotIndex}`"
          @dragover.prevent
          @dragenter.prevent
          @drop="onSlotDrop"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const draggedItem = ref(null)
    const cases = [
      { label: '1', colStart: 1, colSpan: 1, rowSpan: 2, row: 1 },
      { label: '2', colStart: 2, colSpan: 1, rowSpan: 2, row: 1 },
      { label: '3', colStart: 3, colSpan: 1, rowSpan: 2, row: 1 },
      { label: '4', colStart: 4, colSpan: 1, rowSpan: 2, row: 1 },
      { label: '5', colStart: 1, colSpan: 1, rowSpan: 2, row: 2 },
      { label: '6', colStart: 2, colSpan: 2, rowSpan: 2, row: 2 },
      { label: '7', colStart: 4, colSpan: 1, rowSpan: 2, row: 2 },
      { label: '8', colStart: 1, colSpan: 1, rowSpan: 2, row: 3 },
      { label: '9', colStart: 2, colSpan: 1, rowSpan: 2, row: 3 },
      { label: '10', colStart: 3, colSpan: 1, rowSpan: 2, row: 3 },
      { label: '11', colStart: 4, colSpan: 1, rowSpan: 2, row: 3 },
      { label: '12', colStart: 1, colSpan: 1, rowSpan: 2, row: 4 },
      { label: '13', colStart: 2, colSpan: 1, rowSpan: 2, row: 4 },
      { label: '14', colStart: 3, colSpan: 2, rowSpan: 2, row: 4 },
      { label: '15', colStart: 1, colSpan: 1, rowSpan: 2, row: 5 },
      { label: '16', colStart: 2, colSpan: 1, rowSpan: 2, row: 5 },
      { label: '17', colStart: 3, colSpan: 1, rowSpan: 2, row: 5 },
      { label: '18', colStart: 4, colSpan: 1, rowSpan: 2, row: 5 },
    ]

    const getStyle = (slot) => {
      return {
        gridColumn: `${slot.colStart} / span ${slot.colSpan}`,
        gridRow: `span ${slot.rowSpan}`,
      }
    }

    const onDragStart = (e) => {
      draggedItem.value = e.target
      e.dataTransfer.effectAllowed = 'move'
      // You can set custom drag image if needed
      // e.dataTransfer.setDragImage(e.target, 10, 10)
    }

    const onSlotDrop = (e) => {
      e.preventDefault()
      if (draggedItem.value) {
        const slot = e.target
        slot.innerHTML = ''
        slot.appendChild(draggedItem.value)
      }
    }

    return {
      cases,
      getStyle,
      onDragStart,
      onSlotDrop,
    }
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
}

.wood-texture {
  background-image: url('wood-texture5.jpg');
  background-size: repeat;
  width: 100%;
}

.case {
  background-color: transparent;
  border-radius: 3px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  color: #7b3f00;
  gap: 4px;
  flex-wrap: wrap;

  box-shadow:
    inset 0 0 40px rgb(0, 0, 0),
    inset 0 5px 10px rgba(255, 255, 255, 0.1);
  border: 2px solid #3b1d0a;
  position: relative;
}

.case::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.35);
  border-radius: 3px;
  z-index: 0;
}

.case > * {
  position: relative;
  z-index: 1; /* pour que le contenu passe par-dessus */
}

.slot {
  height: 100px;
  width: 26px;
}

.slot:hover {
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.1);
}

.book {
  border: solid 1px #000;
}
</style>
